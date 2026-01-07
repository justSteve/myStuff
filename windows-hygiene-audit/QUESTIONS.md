# Migration Questions

Questions requiring user input before proceeding with fresh Windows installation.

---

## Hardware & BIOS

### Q1: BIOS Update Approach
**Context**: Motherboard BIOS updates can fix bugs, improve stability, and add CPU support, but carry small risk.

**Question**: If a BIOS update is available, do you want to:
- [ ] Update BIOS before fresh Windows install
- [ ] Skip BIOS update (current version working fine)
- [ ] Research the changelog first, then decide

**User Answer**: _pending_

---

### Q2: Disk Health Action
**Context**: If any disk shows degraded health, it should be addressed before installing a fresh OS.

**Question**: If a disk shows health warnings:
- [ ] Replace it before fresh install
- [ ] Note it but proceed (have backups)
- [ ] Run extended diagnostics first

**User Answer**: _pending_

---

## WSL & Containers

### Q3: WSL Distribution Strategy
**Context**: Current WSL distros include `judge0-wsl` and `Ubuntu`. These can be exported and reimported, or rebuilt fresh.

**Question**: What should happen to WSL distributions?
- [ ] Export and reimport after fresh install (preserves customizations)
- [ ] Rebuild from scratch (cleaner, but more setup time)
- [ ] Don't need WSL on the new install
- [ ] Decide per-distro (judge0-wsl vs Ubuntu may differ)

**User Answer**: _pending_

---

### Q4: Docker Strategy
**Context**: Docker Desktop with WSL2 backend. Images and volumes can be exported or rebuilt.

**Question**: Docker approach for fresh install:
- [ ] Export critical images/volumes, reimport after
- [ ] Rebuild from Dockerfiles (cleaner)
- [ ] Don't need Docker on new install
- [ ] Use different container runtime (Podman, etc.)

**User Answer**: _pending_

---

## Data Migration

### Q5: Code Repository Strategy
**Context**: C:\myStuff and C:\myClaude contain git repositories. They can be copied directly or re-cloned from GitHub.

**Question**: How to handle code repositories?
- [ ] Direct copy (preserves local branches, uncommitted work)
- [ ] Re-clone from GitHub (cleaner, but loses unpushed work)
- [ ] Hybrid: push everything first, then re-clone

**User Answer**: _pending_

---

### Q6: Browser Profile Migration
**Context**: Browser profiles contain bookmarks, extensions, saved passwords (if not using Bitwarden), and settings.

**Question**: Browser migration approach:
- [ ] Sign in to browser sync (Chrome/Firefox/Edge account)
- [ ] Export bookmarks manually, start fresh otherwise
- [ ] Copy entire browser profile directory
- [ ] Different approach per browser

**Browsers in use**: _list TBD from inventory_

**User Answer**: _pending_

---

### Q7: Application Settings Worth Preserving
**Context**: Some apps have complex configurations that are tedious to recreate.

**Question**: Which application settings should be explicitly backed up?
- [ ] VS Code (handled by Settings Sync - just sign in)
- [ ] Windows Terminal settings
- [ ] Git global config
- [ ] SSH config
- [ ] Other: ________________

**User Answer**: _pending_

---

## Fresh Install Choices

### Q8: Windows Version
**Context**: Fresh install provides opportunity to choose edition.

**Question**: Which Windows version to install?
- [ ] Windows 11 Pro (current)
- [ ] Windows 11 Home
- [ ] Stay on Windows 10 (if currently on 10)
- [ ] Other: ________________

**User Answer**: _pending_

---

### Q9: Package Manager Strategy
**Context**: Chocolatey is currently installed with many packages. Windows 11 has winget built-in.

**Question**: Package management approach for new install:
- [ ] Primarily winget, Chocolatey only when needed
- [ ] Primarily Chocolatey (familiar workflow)
- [ ] Mix based on what's available where
- [ ] Minimal package manager use (manual installs)

**User Answer**: _pending_

---

### Q10: Python Environment Strategy
**Context**: Current system has multiple Python installations causing confusion.

**Question**: Python setup for new install:
- [ ] pyenv-win (multiple versions, clean management)
- [ ] Single Python.org install (simplest)
- [ ] Anaconda/Miniconda (if doing data science)
- [ ] System Python + venv/uv only

**User Answer**: _pending_

---

### Q11: Node.js Environment Strategy
**Context**: Node version management prevents version conflicts.

**Question**: Node.js setup for new install:
- [ ] fnm (Fast Node Manager) - recommended
- [ ] nvm-windows
- [ ] Single Node.js installer
- [ ] Volta

**User Answer**: _pending_

---

## Secrets & Security

### Q12: API Key Migration
**Context**: Old system had API keys in environment variables (security risk). Fresh install is opportunity to do better.

**Question**: API key management for new install:
- [ ] Bitwarden Secrets Manager (already in use)
- [ ] Azure Key Vault integration
- [ ] .env files with .gitignore (per-project)
- [ ] Keep some in environment variables (which ones?)

**User Answer**: _pending_

---

### Q13: SSH Key Strategy
**Context**: SSH keys are critical for GitHub, servers, etc.

**Question**: SSH key approach:
- [ ] Copy existing keys (same identity, simpler)
- [ ] Generate new keys (opportunity to rotate)
- [ ] Both: copy existing, plan rotation later

**User Answer**: _pending_

---

## Timing & Logistics

### Q14: Old Disk/Partition Handling
**Context**: After fresh install, old Windows partition will exist (if not formatted).

**Question**: What to do with old Windows installation:
- [ ] Full format during install (clean slate)
- [ ] Keep old partition temporarily for file recovery
- [ ] Install on different drive, keep old drive accessible

**User Answer**: _pending_

---

### Q15: Backup Verification
**Context**: Before wiping, need confidence that backups are complete and accessible.

**Question**: Backup destination and verification:
- [ ] External USB drive
- [ ] Cloud storage (OneDrive/Google Drive/etc.)
- [ ] NAS or network location
- [ ] Multiple locations (specify): ________________

**User Answer**: _pending_

---

## Legacy Context (From Previous Hygiene Audit)

The following items were identified during the original hygiene audit and may inform migration decisions:

### Old Data at Root
- `C:\oldWSL\` - Full Linux filesystem backup
- `C:\UbuntuBackup.tar` - Ubuntu backup archive
- Hex-named installer temp folders (safe to ignore for fresh install)

### Software Versions Noted
- Multiple Python installations (will be fresh on new install)
- SQL Server 2019 and 2022 tools (determine which is needed)
- VS 2010/2012 schemas (likely not needed for fresh install)
- Multiple trading applications (tastytrade, TradeStation, thinkorswim)

---

## Response Format

When answering, please use format:
```
Q1: [your choice]
Q2: [your choice]
...
```

Or simply respond conversationally and I'll extract the answers.
