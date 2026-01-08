# Data Migration Checklist

**Generated**: 2026-01-07

This checklist identifies what to migrate, what to reinstall fresh, and what needs decisions.

---

## MIGRATE: Critical Data (Copy to External Storage)

### Code Repositories

| Location | Contents | Size | Action |
|----------|----------|------|--------|
| `C:\myStuff\` | 19 project directories | TBD | **BACKUP** - Push all to GitHub first |
| `C:\myClaude\tooling\` | Claude-related tooling | TBD | **BACKUP** |

**Projects in C:\myStuff:**
- Bitwarden, Daemon, Fabric, IDEasPlatform, MemorySystem
- myDSPy, myFireplace, ParseClipmate, SkillsLogger
- Substrate, Telos, windows-hygiene-audit
- _infra, _meta, _tooling, src
- .beads, .claude, .github (config directories)

**Recommendation**: Run `git status` in each project and push any uncommitted work before backup.

---

### SSH Keys & Certificates

| File | Location | Action |
|------|----------|--------|
| known_hosts | `~\.ssh\known_hosts` | **COPY** - Contains server fingerprints |
| uJudge0_key.pem | `~\.ssh\uJudge0_key.pem` | **COPY** - Critical for Azure VM access |

**Note**: No id_rsa or id_ed25519 found - using GitHub credentials manager instead?

---

### Git Configuration

**Current Global Config:**
```
user.email=steve@juststeve.com
user.name=Steve
core.editor=VS Code
core.autocrlf=input
```

**Action**: Export and recreate manually (simple config)

```powershell
# Export current config
git config --global --list > git-config-backup.txt
```

---

### GitHub Credentials

GitHub credentials stored in Windows Credential Manager:
- `https://github.com/` (generic)
- `git:https://github.com` (git credential helper)
- `gh:github.com:justSteve` (GitHub CLI)
- `GitHub for Visual Studio` (VS integration)

**Action**: After fresh install, sign in to:
1. GitHub CLI (`gh auth login`)
2. VS Code GitHub extension
3. Git credential manager (auto-creates on first push)

---

### Application Settings

| App | Settings Location | Action |
|-----|-------------------|--------|
| VS Code | `%APPDATA%\Code\User\settings.json` | **Settings Sync** - Just sign in |
| Windows Terminal | `%LOCALAPPDATA%\...\WindowsTerminal\...\settings.json` | **COPY** or recreate |
| Git | `~\.gitconfig` | **RECREATE** (3 lines) |

---

## MIGRATE: WSL Distributions (Decision Required)

### Current State

| Distribution | State | Version | Action |
|--------------|-------|---------|--------|
| Ubuntu | Running | WSL 2 | **DECISION NEEDED** |
| docker-desktop | Running | WSL 2 | Auto-created by Docker |
| judge0-wsl | Running | WSL 2 | **DECISION NEEDED** |

### Options

**Option A: Export and Reimport** (preserves customizations)
```powershell
# Before fresh install
wsl --export Ubuntu C:\backup\ubuntu.tar
wsl --export judge0-wsl C:\backup\judge0.tar

# After fresh install
wsl --import Ubuntu C:\wsl\Ubuntu C:\backup\ubuntu.tar
wsl --import judge0-wsl C:\wsl\judge0-wsl C:\backup\judge0.tar
```

**Option B: Rebuild Fresh** (cleaner, more work)
- Install fresh Ubuntu from Microsoft Store
- Rebuild judge0-wsl from scratch

**Recommendation**: Export judge0-wsl (has Judge0 setup), rebuild Ubuntu fresh.

---

## MIGRATE: Docker (Decision Required)

### Current State
- **Containers**: 7
- **Images**: 9
- **Docker Desktop Version**: 29.1.3

### Options

**Option A: Export Critical Images**
```powershell
# List images
docker images

# Save important ones
docker save -o myimage.tar image:tag
```

**Option B: Rebuild from Dockerfiles** (recommended)
- Cleaner approach
- Dockerfiles should be in project repos

**Recommendation**: Don't migrate Docker state. Rebuild containers from Dockerfiles after fresh install.

---

## DO NOT MIGRATE: Fresh Install These

| Component | Reason |
|-----------|--------|
| Python | Multiple messy installations - start fresh with pyenv-win |
| Node.js | 42+ global npm packages - start fresh with fnm |
| .NET SDKs | Install fresh via `winget` or installer |
| Go | Install fresh |
| Chocolatey packages | Rebuild curated list |
| Environment variables | Rebuild cleanly (no API keys in env vars) |
| PATH entries | Let installers manage |
| Old WSL backups | `C:\oldWSL\` and `C:\UbuntuBackup.tar` - delete |

---

## BROWSER MIGRATION

### Current Status
- No Chrome or Firefox profiles detected in standard locations
- Edge likely primary browser (came with Windows)

### Action
- Sign in to browser sync (Microsoft account for Edge)
- Export bookmarks manually as backup
- Extensions reinstall via sync or manually

---

## PRE-MIGRATION SCRIPT

Run this before starting fresh install:

```powershell
# Create backup directory
$backup = "D:\WindowsBackup_$(Get-Date -Format 'yyyy-MM-dd')"
New-Item -ItemType Directory -Path $backup -Force

# 1. Push all git repos (run manually in each)
# cd C:\myStuff\<project> && git status && git push

# 2. Copy SSH keys
Copy-Item -Path "$env:USERPROFILE\.ssh\*" -Destination "$backup\ssh\" -Recurse

# 3. Export git config
git config --global --list > "$backup\git-config.txt"

# 4. Export WSL distributions
wsl --export Ubuntu "$backup\ubuntu.tar"
wsl --export judge0-wsl "$backup\judge0-wsl.tar"

# 5. Copy Windows Terminal settings
$wtSettings = "$env:LOCALAPPDATA\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState"
Copy-Item -Path "$wtSettings\settings.json" -Destination "$backup\windows-terminal-settings.json"

# 6. Copy code directories
robocopy "C:\myStuff" "$backup\myStuff" /E /XD node_modules .git __pycache__ .venv
robocopy "C:\myClaude" "$backup\myClaude" /E /XD node_modules .git __pycache__ .venv

# 7. List installed Chocolatey packages
choco list --local-only > "$backup\choco-packages.txt"

# 8. List npm global packages
npm list -g --depth=0 > "$backup\npm-global.txt"

# 9. List pip packages
pip list > "$backup\pip-packages.txt"

Write-Host "Backup complete at: $backup"
```

---

## POST-INSTALL ORDER

After fresh Windows installation:

1. **Windows Update** - Get all updates first
2. **Drivers** - AMD chipset, Intel I211 network, NVIDIA GPU
3. **Bitwarden** - For all credentials
4. **Git** - `winget install Git.Git`
5. **VS Code** - Sign in for Settings Sync
6. **Windows Terminal** - Restore settings.json
7. **GitHub CLI** - `winget install GitHub.cli` then `gh auth login`
8. **fnm** - Node version manager
9. **pyenv-win** - Python version manager
10. **Docker Desktop** - Fresh install
11. **WSL** - Import or rebuild distributions
12. **Claude Code CLI** - Install fresh

---

## QUESTIONS TO ANSWER (See QUESTIONS.md)

Before proceeding, answer these key questions:

- [ ] Q3: WSL strategy - export/reimport or rebuild?
- [ ] Q4: Docker strategy - export images or rebuild?
- [ ] Q5: Code repos - direct copy or re-clone from GitHub?
- [ ] Q12: API key management - how to handle going forward?
- [ ] Q15: Backup destination - external USB, cloud, or NAS?

---

## SIZE ESTIMATES

| Item | Estimated Size |
|------|----------------|
| C:\myStuff (excluding node_modules, .git) | ~2-5 GB |
| C:\myClaude | ~500 MB |
| WSL exports (Ubuntu + judge0) | ~5-10 GB |
| SSH keys | < 1 MB |
| Settings files | < 10 MB |
| **Total backup size** | ~10-20 GB |

**Recommendation**: Use external USB drive (32GB+) or cloud storage.
