# Hyper-V

## List Vms
```
Get-VM
```

## Copy file to guest VM
```
Copy-VMFile "VM NAME HERE" -SourcePath "C:\changeme" -DestinationPath "C:\changeme" -CreateFullPath -FileSource Host
```
