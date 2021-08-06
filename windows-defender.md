# Windows Defender
All examples are in PowerShell.

For more information, please see the official documentation:
[Microsoft Documentation for Defender](https://docs.microsoft.com/en-us/powershell/module/defender/?view=windowsserver2019-ps)

## Event logs
Get events from `Microsoft-Windows-Windows Defender/Operational`
```
Get-WinEvent -Logname "Microsoft-Windows-Windows Defender/Operational" | Format-List
```

## Get Status

This will list versions of various Microsoft Defender components, last scan times, and the engine's state.
```
Get-MpComputerStatus
```
Example output:
```
PS C:\> Get-MpComputerStatus


AMEngineVersion                 : 1.1.18400.4
AMProductVersion                : 4.18.2107.4
AMRunningMode                   : Normal
AMServiceEnabled                : True
AMServiceVersion                : 4.18.2107.4
AntispywareEnabled              : True
AntispywareSignatureAge         : 0
AntispywareSignatureLastUpdated : 8/6/2021 8:26:13 AM
AntispywareSignatureVersion     : 1.345.70.0
AntivirusEnabled                : True
AntivirusSignatureAge           : 0
AntivirusSignatureLastUpdated   : 8/6/2021 8:26:13 AM
AntivirusSignatureVersion       : 1.345.70.0
BehaviorMonitorEnabled          : True
ComputerID                      : redacted
ComputerState                   : 0
FullScanAge                     : 4294967295
FullScanEndTime                 :
FullScanStartTime               :
IoavProtectionEnabled           : True
IsTamperProtected               : True
IsVirtualMachine                : True
LastFullScanSource              : 0
LastQuickScanSource             : 2
NISEnabled                      : True
NISEngineVersion                : 1.1.18400.4
NISSignatureAge                 : 0
NISSignatureLastUpdated         : 8/6/2021 8:26:13 AM
NISSignatureVersion             : 1.345.70.0
OnAccessProtectionEnabled       : True
QuickScanAge                    : 2
QuickScanEndTime                : 8/3/2021 5:32:03 PM
QuickScanStartTime              : 8/3/2021 5:30:10 PM
RealTimeProtectionEnabled       : True
RealTimeScanDirection           : 0
TamperProtectionSource          : Signatures
TDTStatus                       : N/A
PSComputerName                  :
```

AntivirusEnabled will show True Defender it is enabled, otherwise False.

## Get/Set Preferences
### Get Preferences
```
Get-MpPreference
```

Example Output:
```
PS C:\> Get-MpPreference


AllowDatagramProcessingOnWinServer            : False
AllowNetworkProtectionDownLevel               : False
AllowNetworkProtectionOnWinServer             : False
AttackSurfaceReductionOnlyExclusions          : {N/A: Must be and administrator to view exclusions}
AttackSurfaceReductionRules_Actions           :
AttackSurfaceReductionRules_Ids               :
CheckForSignaturesBeforeRunningScan           : False
CloudBlockLevel                               : 0
CloudExtendedTimeout                          : 0
ComputerID                                    : redacted
ControlledFolderAccessAllowedApplications     : {N/A: Must be and administrator to view exclusions}
ControlledFolderAccessProtectedFolders        :
DisableArchiveScanning                        : False
DisableAutoExclusions                         : False
DisableBehaviorMonitoring                     : False
DisableBlockAtFirstSeen                       : False
DisableCatchupFullScan                        : True
DisableCatchupQuickScan                       : True
DisableCpuThrottleOnIdleScans                 : True
DisableDatagramProcessing                     : False
DisableDnsOverTcpParsing                      : False
DisableDnsParsing                             : False
DisableEmailScanning                          : True
DisableGradualRelease                         : False
DisableHttpParsing                            : False
DisableInboundConnectionFiltering             : False
DisableIntrusionPreventionSystem              :
DisableIOAVProtection                         : False
DisableNetworkProtectionPerfTelemetry         : False
DisablePrivacyMode                            : False
DisableRdpParsing                             : False
DisableRealtimeMonitoring                     : False
DisableRemovableDriveScanning                 : True
DisableRestorePoint                           : True
DisableScanningMappedNetworkDrivesForFullScan : True
DisableScanningNetworkFiles                   : False
DisableScriptScanning                         : False
DisableSshParsing                             : False
DisableTlsParsing                             : False
EnableControlledFolderAccess                  : 0
EnableDnsSinkhole                             : False
EnableFileHashComputation                     : False
EnableFullScanOnBatteryPower                  : False
EnableLowCpuPriority                          : False
EnableNetworkProtection                       : 0
EngineUpdatesChannel                          : 0
ExclusionExtension                            : {N/A: Must be and administrator to view exclusions}
ExclusionIpAddress                            : {N/A: Must be and administrator to view exclusions}
ExclusionPath                                 : {N/A: Must be and administrator to view exclusions}
ExclusionProcess                              : {N/A: Must be and administrator to view exclusions}
ForceUseProxyOnly                             : False
HighThreatDefaultAction                       : 0
LowThreatDefaultAction                        : 0
MAPSReporting                                 : 0
MeteredConnectionUpdates                      : False
ModerateThreatDefaultAction                   : 0
PlatformUpdatesChannel                        : 0
ProxyBypass                                   :
ProxyPacUrl                                   :
ProxyServer                                   :
PUAProtection                                 : 0
QuarantinePurgeItemsAfterDelay                : 90
RandomizeScheduleTaskTimes                    : True
RealTimeScanDirection                         : 0
RemediationScheduleDay                        : 0
RemediationScheduleTime                       : 02:00:00
ReportingAdditionalActionTimeOut              : 10080
ReportingCriticalFailureTimeOut               : 10080
ReportingNonCriticalTimeOut                   : 1440
ScanAvgCPULoadFactor                          : 50
ScanOnlyIfIdleEnabled                         : True
ScanParameters                                : 1
ScanPurgeItemsAfterDelay                      : 15
ScanScheduleDay                               : 0
ScanScheduleQuickScanTime                     : 00:00:00
ScanScheduleTime                              : 02:00:00
SchedulerRandomizationTime                    : 4
SevereThreatDefaultAction                     : 0
SharedSignaturesPath                          :
SignatureAuGracePeriod                        : 0
SignatureBlobFileSharesSources                :
SignatureBlobUpdateInterval                   : 60
SignatureDefinitionUpdateFileSharesSources    :
SignatureDisableUpdateOnStartupWithoutEngine  : False
SignatureFallbackOrder                        : MicrosoftUpdateServer|MMPC
SignatureFirstAuGracePeriod                   : 120
SignatureScheduleDay                          : 8
SignatureScheduleTime                         : 01:45:00
SignaturesUpdatesChannel                      : 0
SignatureUpdateCatchupInterval                : 1
SignatureUpdateInterval                       : 0
SubmitSamplesConsent                          : 0
ThreatIDDefaultAction_Actions                 :
ThreatIDDefaultAction_Ids                     :
TrustLabelProtectionStatus                    : 0
UILockdown                                    : False
UnknownThreatDefaultAction                    : 0
PSComputerName                                :
```

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
