# Driver Version Research

**Generated**: 2026-01-07

---

## Summary

| Component | Current Version | Latest Available | Update Priority |
|-----------|-----------------|------------------|-----------------|
| AMD Chipset | Unknown | 7.11.26.2142 | **HIGH** |
| Intel I211 Network | 12.18.11.1 (2020) | 14.1.5.0 (2024) | **HIGH** |
| NVIDIA GPU | 32.0.15.6094 (2024) | Current | Low |
| Realtek Audio | (check post-install) | - | Medium |

---

## AMD X570 Chipset Drivers

### Current Status
- Current version: Unknown (need to verify post-install)
- May be using Windows default drivers

### Latest Available
| Version | Date | Source |
|---------|------|--------|
| 7.11.26.2142 | Dec 2025 | TechPowerUp |
| 6.10.x.x | 2024 | AMD Official |

### Download
- **AMD Official**: https://www.amd.com/en/support/downloads/drivers.html/chipsets/am4/x570.html
- **Direct**: https://www.amd.com/en/support/chipsets/amd-socket-am4/x570

### Package Includes
- AMD Chipset Drivers
- AMD Ryzen Power Plans (UEFI CPPC2 support)
- AMD GPIO Driver
- AMD PCI Device Driver
- AMD PSP Driver

### Recommendation
**Install fresh after Windows installation** - Do not carry over old chipset drivers.

---

## Intel I211 Gigabit Network

### Current Status
| Property | Value |
|----------|-------|
| Current Version | 12.18.11.1 |
| Current Date | June 14, 2020 |
| Status | **OUTDATED - 4+ years old** |

### Latest Available
| Version | Date | Notes |
|---------|------|-------|
| 14.1.5.0 | Nov 2024 | Latest stable |
| 14.0.5.0 | Nov 2024 | Alternative |

### Download
- **Intel Official**: https://www.intel.com/content/www/us/en/products/sku/64404/intel-ethernet-controller-i211at/downloads.html
- Search for "Intel Ethernet Adapter Complete Driver Pack"

### Known Issues
- I211 has some Windows 11 compatibility quirks
- Intel PROSet software may have issues - consider driver-only install

### Recommendation
**HIGH PRIORITY** - Update after fresh Windows install. The 2020 driver is missing years of bug fixes and performance improvements.

---

## NVIDIA GeForce GTX 750 Ti

### Current Status
| Property | Value |
|----------|-------|
| Architecture | Maxwell 1.0 (GM107) |
| Current Driver | 32.0.15.6094 |
| Driver Date | August 14, 2024 |
| Status | Current |

### Driver Support Status
| Status | Details |
|--------|---------|
| Current Support | Yes - Game Ready Drivers |
| End of Life | **Coming Soon** - R580 branch will be last |
| Security Updates | Will continue after EOL |

### Important Notes
- GTX 750 Ti is Maxwell 1.0, NOT Kepler
- NVIDIA announced R580 driver branch will be last for Maxwell/Pascal/Volta
- This affects GTX 750 Ti, 900 series, 1000 series
- After EOL: security updates only, no new features or game optimizations

### Download
- **NVIDIA Official**: https://www.nvidia.com/Download/index.aspx
- **GeForce Experience**: Auto-updates (optional)

### Recommendation
**LOW PRIORITY** - Current driver is recent. Install fresh NVIDIA driver after Windows install.
Consider:
- GPU upgrade if gaming is a priority
- Current GPU is fine for development work

---

## Realtek High Definition Audio

### Current Status
- Need to verify version after Windows install
- Gigabyte provides Realtek drivers on support page

### Download
- **Gigabyte Support**: Download from motherboard support page
- **Realtek Official**: https://www.realtek.com/en/component/zoo/category/pc-audio-codecs-high-definition-audio-codecs-software

### Recommendation
**MEDIUM PRIORITY** - Windows usually installs working audio drivers. Check Gigabyte page for latest if issues occur.

---

## Intel Wi-Fi 6 AX200

### Current Status
| Property | Value |
|----------|-------|
| Status | "Not Present" in device manager |
| Likely Reason | Disabled in BIOS or not installed |

### Notes
- The X570 AORUS ULTRA does not have onboard Wi-Fi
- AX200 is likely a PCIe/M.2 add-in card
- If needed, verify it's properly seated and enabled in BIOS

### Download (if enabled)
- **Intel Official**: https://www.intel.com/content/www/us/en/download/19351/windows-10-and-windows-11-wi-fi-drivers-for-intel-wireless-adapters.html

---

## Post-Fresh-Install Driver Order

Recommended installation order after Windows install:

1. **AMD Chipset Drivers** (from AMD) - First priority
2. **NVIDIA GPU Driver** (from NVIDIA) - GeForce.com
3. **Intel I211 Network** (from Intel) - Critical update
4. **Realtek Audio** (from Gigabyte or Windows Update) - If needed
5. **Intel Wi-Fi** (from Intel) - If using wireless

### Do NOT Install
- Old drivers from previous Windows installation
- Driver packs from third-party sites (DriverPack, etc.)
- Manufacturer "system utilities" unless needed

---

## Download Links Summary

| Component | URL |
|-----------|-----|
| AMD Chipset | https://www.amd.com/en/support/chipsets/amd-socket-am4/x570 |
| Intel I211 | https://www.intel.com/content/www/us/en/products/sku/64404/intel-ethernet-controller-i211at/downloads.html |
| NVIDIA GPU | https://www.nvidia.com/Download/index.aspx |
| Gigabyte Motherboard | https://www.gigabyte.com/Motherboard/X570-AORUS-ULTRA-rev-11-12/support |
