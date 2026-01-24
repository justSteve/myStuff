# WSL Troubleshooting - 2026-01-24

> **Status**: RESOLVED - WSL filesystem working via `\\wsl.localhost` path. Registry edit was rolled back.

## Initial Problem
- System froze with vmmemWSL CPU pegged
- Caused by long-running VS Code/Claude session in WSL
- User had to force restart

## Root Cause Analysis
- **16GB total RAM** with no WSL memory limits
- **3 WSL distros running**: Ubuntu, docker-desktop, judge0-wsl
- **vmmemWSL consuming ~4.9GB** at session start
- **Only 2.7GB available RAM** - system was memory-starved

## Actions Taken

### 1. Removed Unused WSL Distros
```bash
wsl --unregister judge0-wsl      # Deleted
wsl --unregister docker-desktop  # Later handled by Docker uninstall
```

### 2. Uninstalled Docker Desktop
- Removed from registry startup (kept re-adding itself)
- Full uninstall via: `winget uninstall "Docker Desktop" --silent`
- Service was already set to Manual start

### 3. Created .wslconfig Memory Limits
File: `C:\Users\steve\.wslconfig`
```ini
[wsl2]
memory=8GB
swap=2GB
```

Initial attempt with 6GB + processors=4 + pageReporting=true caused instability.
Simplified to just memory/swap limits with 8GB cap.

### 4. Updated WSL
- Updated from previous version to **2.6.3**
- Command: `wsl --update`

## State After Initial Reboot (4:49 AM)

| Item | Status |
|------|--------|
| WSL Distros | Ubuntu only (Running) |
| Docker Desktop | Uninstalled |
| judge0-wsl | Deleted |
| .wslconfig | 8GB memory, 2GB swap |
| WSL Version | 2.6.3 |

**Problem persisted after reboot** - P9RdrService still not starting.

## Session 2: Additional Fixes Applied

### 1. WSL Updated to 2.7.0
```powershell
wsl --update --pre-release
# Updated from 2.6.3 → 2.7.0
```

### 2. P9NP Registry Fix
Moved P9NP to first position in network provider order (was second after RDPNP):

**Before:**
```
RDPNP,P9NP,LanmanWorkstation,webclient
```

**After:**
```
P9NP,RDPNP,LanmanWorkstation,webclient
```

Registry keys modified (requires elevation):
- `HKLM\SYSTEM\CurrentControlSet\Control\NetworkProvider\Order`
- `HKLM\SYSTEM\CurrentControlSet\Control\NetworkProvider\HwOrder`

### 3. Findings
- **P9RdrService** is a trigger-start service (Manual) that should auto-start when `\\wsl$` is accessed
- The trigger mechanism is broken
- Network Discovery is enabled (not the issue)
- No conflicting drivers (like cbfsconnect2017) found
- **Root cause**: P9NP network provider priority - being second instead of first may prevent proper trigger

## Session 3: Registry Edit Failed - Rolled Back

The P9NP registry edit (moving P9NP to first position) introduced **new errors** rather than fixing the issue. The change was rolled back to original order:

```
RDPNP,P9NP,LanmanWorkstation,webclient
```

## Resolution (2026-01-24)

After multiple reboots and rolling back the registry change, **WSL filesystem access is working**:

| Item | Status |
|------|--------|
| WSL Version | 2.7.0 |
| P9NP Position | Second (original, RDPNP first) |
| P9RdrService | Shows "Stopped" (misleading - see note) |
| `\\wsl.localhost\Ubuntu` | **Working** |
| Windows Explorer | Can navigate WSL tree |
| VS Code Remote-WSL | **Working** |

### Key Finding: P9RdrService Status is Misleading

The `\\wsl.localhost\<distro>` path (introduced in newer WSL versions) appears to use a **different mechanism** than the older `\\wsl$\<distro>` path. P9RdrService showing "Stopped" does not prevent `\\wsl.localhost` access.

**What actually fixed it:**
1. WSL 2.7.0 update
2. Removing unused distros (judge0-wsl, docker-desktop)
3. Memory limits in `.wslconfig` (8GB cap)
4. Rolling back the problematic registry edit
5. Multiple reboots

### Verification (Completed)
- [x] `wsl -l -v` shows Ubuntu Running
- [x] `\\wsl.localhost\Ubuntu\root\projects` accessible in Explorer
- [x] VS Code opens WSL folders correctly
- [x] PowerShell can access path (with proper escaping)

## Reference: Nuclear Options (Not Needed)

These were prepared but **not required** for this resolution.

### Option A: Re-register P9NP manually
```powershell
# Run as admin
rundll32.exe setupapi.dll,InstallHinfSection DefaultInstall 132 C:\Windows\INF\wsl.inf
```

### Option B: Reinstall WSL (preserves Ubuntu data with export)
```powershell
# Export Ubuntu first
wsl --export Ubuntu C:\backup\ubuntu.tar

# Uninstall WSL
wsl --uninstall

# Reinstall from Store or:
wsl --install

# Restore Ubuntu
wsl --import Ubuntu C:\WSL\Ubuntu C:\backup\ubuntu.tar
```

### Option C: Check Windows Event Logs
```powershell
Get-WinEvent -LogName Application -MaxEvents 100 |
  Where-Object { $_.Message -like '*P9*' -or $_.Message -like '*WSL*' } |
  Select TimeCreated, Message
```

## Commands for Future Reference

### Check WSL Health
```powershell
wsl -l -v
wsl --status
Get-Process -Name 'vmmem*'
(Get-CimInstance Win32_OperatingSystem).FreePhysicalMemory / 1MB
```

### If Docker Desktop Sneaks Back
```powershell
Remove-ItemProperty -Path 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Run' -Name 'Docker Desktop'
```

### Reset WSL If Problems
```bash
wsl --shutdown
wsl --update
# Then reboot Windows if \\wsl$ bridge broken
```

## Memory Budget (16GB System)
- Windows + Apps: ~6-8GB
- WSL cap: 8GB
- Buffer: leaves ~2GB headroom for spikes

## Lessons Learned

1. **Don't mess with P9NP registry order** - Moving P9NP ahead of RDPNP caused more problems
2. **Use `\\wsl.localhost` not `\\wsl$`** - Newer path format is more reliable in WSL 2.x
3. **P9RdrService status is misleading** - "Stopped" doesn't mean WSL filesystem is broken
4. **Memory limits matter** - Uncapped WSL on 16GB system will cause freezes
5. **Remove unused distros** - Each running distro consumes resources even when idle
