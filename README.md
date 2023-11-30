# PSWindowsUpdate
This module contain cmdlets to manage Windows Update Client.

## Table of Contents
- [PSWindowsUpdate](#PSWindowsUpdate)
- [Release Notes](#Release-Notes)
- [Install module from the PowerShell Gallery](#Install-module-from-the-PowerShell-Gallery)
- [Usage and Examples](#Usage-and-Examples)
  - [Get-WindowsUpdate / Install-WindowsUpdate](#Get-WindowsUpdate-/-Install-WindowsUpdate)
  - [Add-WUServiceManager](#Add-WUServiceManager)
  - [Get-WUHistory](#Get-WUHistory)
  - [Remove-WindowsUpdate](#Remove-WindowsUpdate)
  - [Get-WUSettings / Set-WUSettings](#-WUSettings-/-Set-WUSettings)
- [Support](#Support)

# Release Notes
v2.2.1  
- Set-WUSettings added params to control TargetRelease for control Feature Updates version and Windows Update for Business
- Fixes Remove-WindowsUpdate bug

v2.2.0  
- New cmdlet Reset-WUComponents, for reset Windows Updates components to default
- New cmdlet Get-WUOfflineMSU, for download offline msu package from microsoft Update Catalog

v2.1.1  
- Remove-WindowsUpdate added WU Api uninstallation mode
- Fixed bug with slow run cmdlets
- Added support for Office 365 users to send emails

v2.1.0  
- New cmdlet Set-PSWUSettings, for save PSWUSettings to xml file
- Param -SendReport can use smtp server credentials
- Install-WindowsUpdate added -RecurseCycle param, to install next updates after reboot
- Install-WindowsUpdate added new pre search criteria: DeploymentAction, IsAssigned, IsPresent, BrowseOnly and AutoSelectOnWebSites
- Change location of PSWindowsUpdate.log file to $Env:TEMP
- Fixed Get-WULastResults bugs
- Fixed Remove-WUServiceManager bugs

v2.0.0 
- Rewrite whole script module to binary module

# Install module from the PowerShell Gallery
```PowerShell
Install-Module PSWindowsUpdate
```

# Usage and Examples
Import the module:
```PowerShell
Import-Module PSWindowsUpdate
```
### Get-WindowsUpdate / Install-WindowsUpdate
Get windows updates available from default service manager.
```PowerShell
Get-WindowsUpdate
```

Get all available update on remote machine MG-PC, that contains in Title this two words 'Aktualizacja' and 'Windows 11' (as regular expression).
```PowerShell
Get-WindowsUpdate -ComputerName MG-PC -MicrosoftUpdate -Title "Aktualizacja.*Windows 11" -Verbose
```

Hide update with KBArticleID: KB4034658.
```PowerShell
Get-WindowsUpdate -KBArticleID KB4034658 -Hide -Verbose
```
...or use alias
```PowerShell
Hide-WindowsUpdate -KBArticleID KB4034658 -Verbose
```

Schedule job at 6:00 PM to install update with UpdateId='ddb74579-7a1f-4d1f-80c8-e8647055314e' and RevisionNumber=200. Update will be automaticaly accepted and after all serwer will be automaticaly restarted if needed.
```PowerShell
Get-WindowsUpdate -MicrosoftUpdate -UpdateID ddb74579-7a1f-4d1f-80c8-e8647055314e -RevisionNumber 200 -ScheduleJob (Get-Date -Hour 18 -Minute 0 -Second 0) -Install -AcceptAll -AutoReboot -Verbose
```
...or use alias
```PowerShell
Install-WindowsUpdate -MicrosoftUpdate -UpdateID ddb74579-7a1f-4d1f-80c8-e8647055314e -RevisionNumber 200 -ScheduleJob (Get-Date -Hour 18 -Minute 0 -Second 0) -AcceptAll -AutoReboot -Verbose
```

### Add-WUServiceManager
Try register Microsoft Update service as Service Manager.
```PowerShell
Add-WUServiceManager -MicrosoftUpdate
```

Try register Offline Sync Service from file C:\wsusscn2.cab.
```PowerShell
Add-WUServiceManager -ScanFileLocation C:\wsusscn2.cab
```

### Get-WUHistory
Get Windows Update history.
```PowerShell
Get-WUHistory
```

Get Windows Update Agent history for last 24h.
```PowerShell
Get-WUHistory -MaxDate (Get-Date).AddDays(-1)
```

### Remove-WindowsUpdate
Try to uninstall update with specific KBArticleID = KB958830.
```PowerShell
Get-WUUninstall -KBArticleID KB958830
```

### Get-WUSettings / Set-WUSettings
Get current Windows Update Client configuration.
```PowerShell
Get-WUSettings
```

Set the target version for feature updates to Windows 10 22H2.
```PowerShell
Set-WUSettings -TargetReleaseVersion -TargetReleaseVersionInfo 22H2 -ProductVersion "Windows 10"
```

# Support
I develop most of my code under open licenses, free of charge.
If you are satisfied with these solutions, you can express your [support for me](https://github.com/mgajda83/PSWindowsUpdate/assets/47522674/da5e45e2-f73d-4190-96a3-c838208be9f2).
The greater your support, the greater the motivation to develop them further. The more motivation, the more things I can create.
