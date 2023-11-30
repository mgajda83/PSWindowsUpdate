# PSWindowsUpdate
This module contain cmdlets to manage Windows Update Client.

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

