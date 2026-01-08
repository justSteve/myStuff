# BIOS Research - Gigabyte X570 AORUS ULTRA

**Generated**: 2026-01-07

---

## Current BIOS

| Property | Value |
|----------|-------|
| Model | Gigabyte X570 AORUS ULTRA (rev 1.1/1.2) |
| Current Version | **F37f** |
| Current Date | 2023-09-20 |
| BIOS Vendor | American Megatrends International |

---

## Available BIOS Updates

Based on community reports and forum discussions:

| Version | Date | AGESA | Notes |
|---------|------|-------|-------|
| F37f | 2023-09-20 | 1.2.0.7+ | **Currently installed** |
| F37g | 2023-10 | 1.2.0.B | Fixes "Inception" vulnerability |
| F37h | 2023-12 | 1.2.0.B+ | Reported then removed from website |
| F38 (beta) | 2024-07-30 | 1.2.0.CB | Fixes "Sinkclose" vulnerability (CVE-2024-36877) |

**Note**: Gigabyte has been inconsistent with X570 BIOS availability - versions sometimes appear and disappear from the download page.

---

## Security Vulnerabilities Addressed

### Sinkclose (CVE-2024-36877) - July 2024
- Affects AMD processors including Ryzen 5000 series
- Allows privilege escalation to SMM (System Management Mode)
- Fixed in AGESA ComboAM4v2PI 1.2.0.CB
- **F38 beta addresses this**

### Inception (CVE-2023-20569) - August 2023
- Speculative execution side-channel attack
- Fixed in AGESA 1.2.0.B
- **F37g and later address this**

### fTPM Stutter Fix
- Random stuttering caused by fTPM
- Fixed in AGESA 1.2.0.7 (F37 series)
- **F37f includes this fix**

---

## Recommendation

| Priority | Action |
|----------|--------|
| **HIGH** | Update to F38 or latest available for Sinkclose fix |
| Medium | If F38 unavailable, use F37g for Inception fix |
| Low | Current F37f is acceptable if security not critical |

### Before Updating

1. Download BIOS file to USB FAT32 drive
2. Use Q-Flash (in BIOS) or @BIOS (Windows utility)
3. **DO NOT interrupt the update process**
4. Clear CMOS after update if instability occurs

### Where to Download

- **Official**: https://www.gigabyte.com/Motherboard/X570-AORUS-ULTRA-rev-11-12/support#support-dl-bios
- **AORUS Site**: https://www.aorus.com/motherboards/X570-AORUS-ULTRA-rev-11-12/Support
- **Backup**: Check TweakTown forums for archived versions if official site removes them

---

## Post-Install BIOS Settings

After fresh Windows install, consider these BIOS optimizations:

1. **Enable DOCP/XMP** - RAM is DDR4-3600 but running at 2133 MHz
2. **Verify fTPM is enabled** - Required for Windows 11
3. **Check Secure Boot** - Enable for Windows 11 compliance
4. **Resizable BAR** - Enable if GPU supports it (GTX 750 Ti does not)
5. **AMD CBS → Global C-state Control** - Enable for power savings

---

## Notes

- Current F37f is from Sept 2023 - about 1.5 years old
- The Sinkclose vulnerability is serious but requires existing admin access to exploit
- For a fresh install, updating BIOS *before* install is recommended
- Keep a backup of F37f BIOS file in case rollback needed
