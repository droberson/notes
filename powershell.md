# PowerShell

## Get Version
```
$PSVersionTable
```

Example output:
```
PS C:\> $PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.19041.1023
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
BuildVersion                   10.0.19041.1023
CLRVersion                     4.0.30319.42000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

## Logging
TODO: this
### Enabling
### Disabling
### Event Logs
`Microsoft-Windows-Powershell/Operational`

## Execution Policy
TODO: this

## Specify Version
Sometimes, it may be useful to run a specific version of PowerShell. For example, you may be 
developing scripts meant to run on older hosts servers on your flashy, modern, patched, and up
to date developer workstation. Since new features are introduced in each PowerShell release,
it makes sense to test with the intended version. Running scripts meant for the wrong version
of PowerShell can cause spectacular failures.

This may require installing additional versions of the .NET Framework on the host system.

### Run as PowerShell 2
```
powershell.exe -Version 2
```

## LNK Files
```powershell
function Dump-LNK($FullPath) {
    $sh = New-Object -ComObject Wscript.Shell
    $lnk = $sh.CreateShortcut($FullPath)
    $lnk
}

function Get-LNKsInPath($Path, $Pattern) {
    $LNKs = Get-ChildItem -Path $Path -Recurse -Force -Filter "*.lnk" -ErrorAction SilentlyContinue
    foreach ($LNK in $LNKs) {
        $t = Dump-LNK($LNK.FullName)
        if ($Pattern -ne $null) {
            if ($t.TargetPath.Contains($Pattern) -or $t.ARguments.Contains($Pattern)) { $t }
        } else {
            $t
        }
    }
}

function Get-LNKsInPathOnlyPath($Path, $Pattern) {
    $LNKs = Get-ChildItem -Path $Path -Recurse -Force -Filter "*.lnk" -ErrorAction SilentlyContinue
    foreach ($LNK in $LNKs) {
        $t = Dump-LNK($LNK.FullName)
        if ($Pattern -ne $null) {
            if ($t.TargetPath.Contains($Pattern) -or $t.ARguments.Contains($Pattern)) { $t.FullName }
        } else {
            $t.FullName
        }
    }
}

Get-LNKsInPath -Path "C:\users\"  -Pattern "malware"
```
