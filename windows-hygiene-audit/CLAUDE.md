# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

This is a **hardware inventory and migration preparation project** for a fresh Windows installation. The focus has shifted from optimizing the existing environment to:

1. **Hardware Inventory**: Document all hardware components (motherboard, CPU, GPU, storage, peripherals)
2. **Driver/BIOS Research**: Identify available updates for motherboard, chipset, BIOS, and other infrastructure
3. **Migration Planning**: Determine what data/configurations to migrate vs. start fresh
4. **Pre-Install Checklist**: Ensure hardware is ready for a clean Windows installation

**CRITICAL: This is primarily a research and documentation project. Hardware changes require explicit user approval.**

## Current System Hardware (To Be Inventoried)

### Key Information Needed
- Motherboard make/model and current BIOS version
- CPU model and microcode version
- GPU model and current driver version
- Storage devices (SSDs, HDDs) - health status and capacity
- RAM configuration
- Network adapters (wired/wireless)
- Audio devices
- USB controllers and connected peripherals

## Commands for Hardware Inventory (Read-Only)

```powershell
# System overview
systeminfo

# Motherboard/BIOS info
Get-WmiObject Win32_BaseBoard | Select Manufacturer, Product, SerialNumber
Get-WmiObject Win32_BIOS | Select Manufacturer, SMBIOSBIOSVersion, ReleaseDate

# CPU info
Get-WmiObject Win32_Processor | Select Name, NumberOfCores, NumberOfLogicalProcessors

# GPU info
Get-WmiObject Win32_VideoController | Select Name, DriverVersion, DriverDate

# Storage devices
Get-PhysicalDisk | Select FriendlyName, MediaType, Size, HealthStatus
Get-Disk | Select Number, FriendlyName, Size, PartitionStyle

# RAM
Get-WmiObject Win32_PhysicalMemory | Select BankLabel, Capacity, Speed, Manufacturer

# Network adapters
Get-NetAdapter | Select Name, InterfaceDescription, Status, MacAddress

# All devices (verbose)
Get-PnpDevice -Status OK | Select Class, FriendlyName, InstanceId

# Check driver versions for all devices
Get-WmiObject Win32_PnPSignedDriver | Select DeviceName, DriverVersion, DriverDate | Sort DeviceName
```

## Migration Considerations

### Data to Migrate
- User documents and files (C:\myStuff, C:\myClaude)
- SSH keys and certificates
- Browser profiles/bookmarks
- Application settings worth preserving

### Fresh Start (Don't Migrate)
- Python installations (install fresh)
- Node.js (install fresh with nvm or fnm)
- .NET SDKs (install fresh)
- Chocolatey packages (rebuild from curated list)
- Environment variables (recreate cleanly)
- PATH entries (build fresh)

### Research Required
- Current BIOS version vs. latest available
- Chipset drivers - current vs. latest
- Storage controller drivers
- Any known hardware issues or firmware updates

## File Structure

```
windows-hygiene-audit/
  CLAUDE.md             # This file - project guidance
  MIGRATION-PLAN.md     # Phased migration/fresh install plan
  QUESTIONS.md          # Questions needing user input
  inventory/            # Hardware and software inventory outputs
    hardware-inventory.md
    driver-versions.md
    bios-research.md
    migration-checklist.md
```

## Safety Protocol

1. **Read-only by default**: Gather information without making changes
2. **User approval required**: No BIOS updates, driver changes, or deletions without explicit confirmation
3. **Document everything**: All findings logged to inventory/ folder
4. **Backup critical data**: Ensure important files are backed up before any system changes
5. **Test hardware health**: Check disk health and memory before fresh install
