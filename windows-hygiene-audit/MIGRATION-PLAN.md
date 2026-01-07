# Fresh Windows Installation - Migration Plan

## Overview

This plan prepares for a fresh Windows installation by inventorying hardware, researching driver/BIOS updates, and determining what to migrate vs. reinstall fresh.

## Phase 1: Hardware Inventory

**Goal**: Document all hardware components and current driver/firmware versions.

### Tasks
- [ ] Gather motherboard make/model and BIOS version
- [ ] Document CPU model
- [ ] Document GPU model and driver version
- [ ] List all storage devices with health status
- [ ] Document RAM configuration
- [ ] List network adapters (wired and wireless)
- [ ] Document audio devices
- [ ] List USB controllers and key peripherals
- [ ] Export full device list with driver versions

### Output
- `inventory/hardware-inventory.md` - Complete hardware list

---

## Phase 2: BIOS & Driver Research

**Goal**: Identify available updates for motherboard, chipset, and key components.

### Tasks
- [ ] Look up motherboard manufacturer support page
- [ ] Compare current BIOS version to latest available
- [ ] Check for chipset driver updates
- [ ] Check for storage controller updates (NVMe, SATA)
- [ ] Check for network adapter driver updates
- [ ] Check GPU driver update path (fresh install recommended)
- [ ] Note any known issues or critical updates

### Output
- `inventory/bios-research.md` - BIOS update availability and notes
- `inventory/driver-versions.md` - Current vs. available driver versions

---

## Phase 3: Data Migration Planning

**Goal**: Identify what data/settings to preserve vs. start fresh.

### Migrate (Copy to external/cloud)
- [ ] C:\myStuff\ - All project code and repos
- [ ] C:\myClaude\ - Claude-related projects
- [ ] SSH keys (~\.ssh\)
- [ ] GPG keys if any
- [ ] Browser bookmarks and settings (export)
- [ ] Critical application settings (list TBD)
- [ ] Any licensed software keys/activation info

### Do NOT Migrate (Reinstall Fresh)
- Python environments and installations
- Node.js and npm global packages
- .NET SDKs
- Chocolatey and all packages
- Go installation
- Git (reinstall, config is simple)
- VS Code (reinstall, Settings Sync handles config)
- Environment variables (rebuild cleanly)
- PATH entries (rebuild from scratch)

### Uncertain (Needs Decision)
- WSL distributions (judge0-wsl, Ubuntu) - rebuild or migrate?
- Docker images and volumes
- Database data (if any local DBs)
- Bitwarden local vault data

### Output
- `inventory/migration-checklist.md` - What to backup and how

---

## Phase 4: Pre-Install Verification

**Goal**: Ensure hardware is healthy before wiping.

### Tasks
- [ ] Check all disk health (SMART status)
- [ ] Run memory diagnostics
- [ ] Verify backup of critical data is complete and accessible
- [ ] Download Windows installation media
- [ ] Download critical drivers to USB (network, storage if needed)
- [ ] Document Windows license key / Microsoft account link
- [ ] Note WiFi password and network settings

### Output
- `inventory/pre-install-checklist.md` - Final verification before install

---

## Phase 5: Fresh Installation

**Goal**: Clean Windows install with modern, minimal tooling.

### Post-Install Setup Order
1. Windows Update (all updates)
2. Motherboard/chipset drivers (if not auto-installed)
3. GPU drivers (from manufacturer)
4. Bitwarden (for credentials)
5. Git
6. VS Code + Settings Sync
7. Windows Terminal
8. Claude Code CLI
9. Development tools as needed (Python via pyenv, Node via fnm, etc.)

### Modern Tool Choices
| Old Approach | New Approach |
|--------------|--------------|
| Multiple Python installs | pyenv-win or single install |
| Node.js installer | fnm (Fast Node Manager) |
| Chocolatey for everything | winget + selective Chocolatey |
| Manual PATH management | Let installers manage, audit periodically |

---

## Timeline

This is a preparation plan - actual installation date TBD based on:
- Completion of hardware inventory
- BIOS/driver research
- Data backup verification
- User schedule

---

## Notes

- The old `HYGIENE-PLAN.md` focused on cleaning the existing install
- This new plan assumes a fresh start is more efficient than deep cleanup
- All decisions logged in `QUESTIONS.md` for user input
