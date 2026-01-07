# PATH Analysis

## USER PATH Entries (as captured 2026-01-07)

Each entry listed with validation status (to be filled in):

```
[ ] C:\Program Files\PowerShell\7
[ ] c:\Users\steve\AppData\Local\Programs\cursor\resources\app\bin  <-- DUPLICATE
[ ] C:\Program Files (x86)\Microsoft\Edge\Application
[ ] C:\WINDOWS\system32
[ ] C:\WINDOWS
[ ] C:\WINDOWS\System32\Wbem
[ ] C:\WINDOWS\System32\WindowsPowerShell\v1.0\
[ ] C:\WINDOWS\System32\OpenSSH\
[ ] C:\Program Files\Microsoft SQL Server\150\Tools\Binn\
[ ] C:\Program Files\Git\cmd
[ ] C:\Program Files (x86)\Microsoft SQL Server\160\Tools\Binn\
[ ] C:\Program Files\Microsoft SQL Server\160\Tools\Binn\
[ ] C:\Program Files\Microsoft SQL Server\160\DTS\Binn\
[ ] C:\Program Files (x86)\Microsoft SQL Server\160\DTS\Binn\
[ ] C:\ProgramData\chocolatey\bin
[ ] C:\Program Files\OpenSSL\bin
[ ] C:\Program Files\GitHub CLI\
[ ] C:\Users\steve\AppData\Local\Programs\Python\Python312\Scripts\
[ ] C:\Users\steve\AppData\Local\Programs\Python\Python312\  <-- DUPLICATE
[ ] C:\Users\steve\AppData\Local\Microsoft\WindowsApps
[ ] C:\Program Files\nodejs\
[ ] C:\Users\steve\OneDrive\Tools
[ ] C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\170\Tools\Binn\
[ ] C:\Program Files\dotnet\
[ ] C:\Program Files\PowerShell\7\
[ ] C:\Users\steve\AppData\Local\Programs\Python\Python312\  <-- DUPLICATE (3rd occurrence!)
[ ] C:\Users\steve\AppData\Local\Microsoft\WindowsApps  <-- DUPLICATE
[ ] C:\Users\steve\AppData\Local\Programs\Microsoft VS Code\bin
[ ] C:\Program Files\Azure Data Studio\bin
[ ] C:\Users\steve\.dotnet\tools  <-- DUPLICATE
[ ] C:\Users\steve\AppData\Local\Programs\cursor\resources\app\bin  <-- DUPLICATE
[ ] C:\Users\steve\AppData\Roaming\Python\Scripts
[ ] C:\Users\steve\AppData\Roaming\npm
[ ] C:\Users\steve\.dotnet\tools  <-- DUPLICATE
[ ] C:\Users\steve\.local\bin  <-- DUPLICATE
[ ] C:\Users\steve\.local\bin  <-- DUPLICATE
[ ] C:\Users\steve\AppData\Local\Programs\Antigravity\bin
[ ] C:\Users\steve\go\bin
[ ] C:\Users\steve\.bun\bin
```

## Duplicates Summary

| Entry | Occurrences |
|-------|-------------|
| Python312 | 3 |
| .dotnet\tools | 2 |
| cursor bin | 2 |
| .local\bin | 2 |
| WindowsApps | 2 |
| PowerShell\7 | 2 |

## Recommended Deduplicated PATH

```
C:\Program Files\PowerShell\7
C:\Users\steve\AppData\Local\Programs\cursor\resources\app\bin
C:\Program Files (x86)\Microsoft\Edge\Application
C:\WINDOWS\system32
C:\WINDOWS
C:\WINDOWS\System32\Wbem
C:\WINDOWS\System32\WindowsPowerShell\v1.0\
C:\WINDOWS\System32\OpenSSH\
C:\Program Files\Microsoft SQL Server\150\Tools\Binn\
C:\Program Files\Git\cmd
C:\Program Files (x86)\Microsoft SQL Server\160\Tools\Binn\
C:\Program Files\Microsoft SQL Server\160\Tools\Binn\
C:\Program Files\Microsoft SQL Server\160\DTS\Binn\
C:\Program Files (x86)\Microsoft SQL Server\160\DTS\Binn\
C:\ProgramData\chocolatey\bin
C:\Program Files\OpenSSL\bin
C:\Program Files\GitHub CLI\
C:\Users\steve\AppData\Local\Programs\Python\Python312\Scripts\
C:\Users\steve\AppData\Local\Programs\Python\Python312\
C:\Users\steve\AppData\Local\Microsoft\WindowsApps
C:\Program Files\nodejs\
C:\Users\steve\OneDrive\Tools
C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\170\Tools\Binn\
C:\Program Files\dotnet\
C:\Users\steve\AppData\Local\Programs\Microsoft VS Code\bin
C:\Program Files\Azure Data Studio\bin
C:\Users\steve\.dotnet\tools
C:\Users\steve\AppData\Roaming\Python\Scripts
C:\Users\steve\AppData\Roaming\npm
C:\Users\steve\.local\bin
C:\Users\steve\AppData\Local\Programs\Antigravity\bin
C:\Users\steve\go\bin
C:\Users\steve\.bun\bin
```

This removes 8 duplicate entries while preserving all unique paths.

## Entries to Validate Exist

Run this PowerShell to check which paths actually exist:

```powershell
$paths = @(
    "C:\Program Files\PowerShell\7",
    "C:\Users\steve\AppData\Local\Programs\cursor\resources\app\bin",
    # ... add all paths
)

foreach ($p in $paths) {
    $exists = Test-Path $p
    Write-Host "$exists`t$p"
}
```

## Potential Dead Paths (to verify)

These should be checked to see if they still exist:
- `C:\Program Files\Microsoft SQL Server\150\Tools\Binn\` - SQL 2019, may be stale
- `C:\Users\steve\OneDrive\Tools` - Custom tools folder
- `C:\Users\steve\AppData\Local\Programs\Antigravity\bin` - Unknown tool
