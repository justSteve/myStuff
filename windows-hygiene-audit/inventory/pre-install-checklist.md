# Pre-Install Verification Checklist

**Generated**: 2026-01-07

Final verification before fresh Windows installation.

---

## Hardware Health Status

### All Disks: HEALTHY

| Disk | Model | Type | Size | Health | Status |
|------|-------|------|------|--------|--------|
| 0 | Samsung SSD 980 PRO 1TB | NVMe SSD | 931 GB | **Healthy** | Online |
| 1 | Samsung SSD 970 PRO 512GB | NVMe SSD | 477 GB | **Healthy** | Online |
| 2 | WDC WD1002FAEX-00Y9A0 | HDD | 931 GB | **Healthy** | Online |

### Volume Layout

| Drive | Label | Size | Free | Health | Notes |
|-------|-------|------|------|--------|-------|
| C: | (System) | 930 GB | 448 GB | Healthy | Windows + Programs |
| E: | wTera | 644 GB | 320 GB | Healthy | Data partition (HDD) |
| F: | (unlabeled) | 476 GB | **9 MB** | Healthy | **NEARLY FULL** - 970 PRO |
| G: | New Volume | 287 GB | 197 GB | Healthy | Data partition (HDD) |

**WARNING**: F: drive is nearly full (9 MB free). Verify nothing critical is stored there, or clean up before backup.

---

## Windows License Information

| Property | Value |
|----------|-------|
| Edition | **Windows 10 Pro** |
| Architecture | 64-bit |
| Registered To | steve@juststeve.com |
| License Type | Digital license (linked to Microsoft account) |

**Note**: Windows 10 Pro digital license is tied to Microsoft account. After fresh install, sign in with same Microsoft account to activate automatically.

### Upgrade Option
- Windows 11 Pro is a free upgrade from Windows 10 Pro
- Same Microsoft account will activate Windows 11

---

## Network Configuration

### Primary Connection (Ethernet)

| Setting | Value |
|---------|-------|
| Adapter | Intel I211 Gigabit |
| IP Address | 192.168.0.2 |
| Subnet | 255.255.255.0 |
| Gateway | 192.168.0.1 |
| DHCP | Likely (standard home network range) |

### Virtual Adapters (Auto-Created)
- vEthernet (Default Switch) - Hyper-V
- vEthernet (WSL) - WSL2

These will be recreated automatically when Hyper-V/WSL are reinstalled.

---

## Pre-Install Verification Checklist

### Data Backup Verification

- [ ] All git repos pushed to GitHub (check `git status` in each)
- [ ] SSH keys copied to external storage (`~\.ssh\`)
- [ ] Windows Terminal settings backed up
- [ ] WSL distributions exported (if keeping)
- [ ] Critical documents verified on backup

### Hardware Verification

- [x] All disks report **Healthy**
- [x] No SMART errors detected
- [ ] Run Windows Memory Diagnostic (optional but recommended)
- [ ] Verify backup drive is accessible and has space

### Account & License Verification

- [x] Windows license type confirmed (Digital, Microsoft account)
- [x] Microsoft account email noted: steve@juststeve.com
- [ ] Bitwarden vault accessible (for all passwords)
- [ ] GitHub 2FA recovery codes accessible

### Installation Media

- [ ] Windows 11 (or 10) USB installer created
- [ ] Download from: https://www.microsoft.com/software-download/windows11
- [ ] USB drive: minimum 8GB, FAT32 format

### Drivers Ready

- [ ] Downloaded to USB (optional but recommended):
  - Intel I211 network driver (in case Windows doesn't auto-install)
  - NVIDIA GPU driver (can download after, but good to have)
  - AMD chipset drivers

---

## Memory Diagnostic (Optional)

To run Windows Memory Diagnostic:

```powershell
# Schedule memory test (will reboot)
mdsched.exe
```

Or from Start Menu: Search "Windows Memory Diagnostic"

---

## Final Pre-Install Steps

### Day Before Install

1. **Push all code**
   ```powershell
   cd C:\myStuff
   Get-ChildItem -Directory | ForEach-Object {
     Write-Host "Checking $_"
     cd $_.FullName
     git status
     cd ..
   }
   ```

2. **Run backup script** (from migration-checklist.md)

3. **Verify backup is complete and readable**

4. **Export WSL** (if keeping)
   ```powershell
   wsl --export judge0-wsl D:\backup\judge0-wsl.tar
   ```

### Day of Install

1. **Disconnect unnecessary drives** (optional safety measure)
   - Can physically disconnect HDD during install
   - Prevents accidental formatting

2. **Boot from USB installer**
   - F12 or F2 during POST for boot menu (varies by BIOS)
   - Gigabyte: Usually F12

3. **Choose installation target**
   - Recommended: Format C: drive only
   - Or: Full format for completely clean start

4. **First boot tasks**
   - Complete OOBE (Out of Box Experience)
   - Sign in with Microsoft account
   - Run Windows Update
   - Install drivers (chipset → GPU → network)

---

## Post-Install Verification

After fresh install, verify:

- [ ] Windows activated (Settings → System → Activation)
- [ ] All disks visible and accessible
- [ ] Network connected
- [ ] Can access backup files
- [ ] Can sign into Microsoft account
- [ ] Can sign into GitHub

---

## Emergency Recovery

If something goes wrong:

1. **Boot from USB installer** → Repair options
2. **Access command prompt** → Can browse drives
3. **Recovery partition** → If still present

### Important Paths on Old Drive (if accessible)
- `C:\myStuff\` - Code repositories
- `C:\Users\steve\.ssh\` - SSH keys
- `C:\Users\steve\AppData\Roaming\Code\User\` - VS Code settings

---

## Summary

| Check | Status |
|-------|--------|
| Disk Health | **PASS** - All healthy |
| Windows License | **PASS** - Digital license, Microsoft account |
| Network Info | **PASS** - Documented |
| Backup Plan | **READY** - See migration-checklist.md |

**System is ready for fresh Windows installation.**

Recommended installation: **Windows 11 Pro** (free upgrade, same license)
