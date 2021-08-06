# Windows Defender
All examples are in PowerShell.

For more information, please see the official documentation:
[Microsoft Documentation for Defender](https://docs.microsoft.com/en-us/powershell/module/defender/?view=windowsserver2019-ps)

## Event logs
TODO: this

## Get Status

This will list versions of various Microsoft Defender components, last scan times, and the engine's state.

```
Get-MpComputerStatus
```
TODO: output

AntivirusEnabled will show True if it is enabled, otherwise False.

## Get/Set Preferences
### Get Preferences
```
Get-MpPreference
```
TODO: output

### Set Preferences
```
Set-MpPreference -PREFERENCE Setting
```

## Exclusions
Sometimes, malware or attackers may make malicious configurations to exclude directories.

Smart attackers may store malware in pre-existing, legitimate exclusion directories.

### Exclude a directory
```
Set-MpPreference -ExclusionPath C:\malware-samples\
```

### Remove a directory exclusion
```
Remove-MpPreference -ExclusionPath C:\malware-samples\
```

### Exclude a file type
```
Set-MpPreference -ExclusionExtension EXT
```


## Manual Scans

### Quick Scan
```
Start-MpScan -ScanType QuickScan
```

### Full Scan
```
Start-MpScan -ScanType FullScan
```

### Scanning a Directory
```
Start-MpScan -ScanType CustomScan -ScanPath C:\Path
```

### Offline Scan
Requires rebooting.
```
Start-MpWDOScan
```

### Schedule a Quick Scan
```
Set-MpPreference -ScanScheduleQuickScanTime TIME
```

### Schedule a Full Scan
```
Set-MpPreference -ScanParameters 2
Set-MpPreference -RemediationScheduleDay [0=Daily, 1-Sunday...7=Saturday, 8=Never]
Set-MpPreference -RemediationScheduleTime TIME
```

## Remove Threats

### All Threats
```
Remove-MpThreat
```

### Remote Computer
```
Remove-MpThreat -CimSession CIMSESSION
```

## Update Signatures
```
Update-MpSignature
```

## External Drive Scanning
```
Set-MpPreference -DisableRemovableDriveScanning $false
```

## Scan Archives (zip, cab, ..)
### Enable
```
Set-MpPreference -DisableArchiveScanning $true
```

### Disable
```
Set-MpPreference -DisableArchiveScanning $false
```

## Scan Network Drives
### Enable
```
Set-MpPreference -DisableScanningMappedNetworkDrivesForFullScan $false
```
### Disable
```
Set-MpPreference -DisableScanningMappedNetworkDrivesForFullScan $true
```

## Disable Until Next Reboot
```
Set-MpPreference -DisableRealtimeMonitoring $true
```
