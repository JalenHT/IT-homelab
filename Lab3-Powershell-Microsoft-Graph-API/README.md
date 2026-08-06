# Lab 4 — PowerShell & Microsoft Graph API

## Objective
Use PowerShell and the Microsoft Graph API to manage 
users and groups in Microsoft Entra ID programmatically,
simulating real enterprise IAM automation.

## Environment
- Microsoft Entra ID Free tier
- PowerShell 7.6.0
- Microsoft Graph PowerShell SDK
- Visual Studio Code

## What I did

### Setup
- Installed PowerShell 7.6.0
- Installed Microsoft Graph module via Install-Module
- Connected to Entra tenant using Connect-MgGraph
- Authenticated with a Global Administrator account

### Queries
- Retrieved all users in the tenant using Get-MgUser
- Retrieved all groups and their types using Get-MgGroup
- Confirmed HR-Finance-Collab is a Unified (M365) group
- Confirmed IT-Staff is a Security group

### User lifecycle automation
- Created a new user (PowerShell User) entirely from 
  PowerShell using New-MgUser
- Disabled the user using Update-MgUser -AccountEnabled:$false
- Confirmed disabled status by querying AccountEnabled property

## What I observed
- PowerShell Graph module requires specific scopes 
  declared at connection time
- User creation via PowerShell is instant and returns 
  the Object ID automatically
- Disabling a user via PowerShell is the same as 
  unchecking Account Enabled in the portal
- This is how IAM teams automate onboarding and 
  offboarding at scale instead of manually clicking 
  through the portal

## Scripts used

### Connect to Graph
```powershell
Connect-MgGraph -Scopes "User.Read.All","Group.ReadWrite.All","User.ReadWrite.All"
```

### Get all users
```powershell
Get-MgUser | Select-Object DisplayName, UserPrincipalName
```

### Get all groups
```powershell
Get-MgGroup | Select-Object DisplayName, GroupTypes
```

### Create a user
```powershell
$PasswordProfile = @{
    Password = "TempPass123!"
    ForceChangePasswordNextSignIn = $false
}
New-MgUser `
    -DisplayName "PowerShell User" `
    -UserPrincipalName "psuser@yourdomain.onmicrosoft.com" `
    -AccountEnabled `
    -PasswordProfile $PasswordProfile `
    -MailNickname "psuser"
```

### Disable a user
```powershell
$user = Get-MgUser -Filter "userPrincipalName eq 'psuser@yourdomain.onmicrosoft.com'"
Update-MgUser -UserId $user.Id -AccountEnabled:$false
```

## Skills demonstrated
- PowerShell 7 scripting
- Microsoft Graph API authentication
- Tenant-wide user and group queries
- Automated user provisioning via PowerShell
- Automated user deprovisioning via PowerShell
- Scope-based permission management

## Tools used
- PowerShell 7.6.0
- Microsoft Graph PowerShell SDK
- Visual Studio Code
- Microsoft Entra ID

## Screenshots
![Get-MgUser Output](get-mguser.png)
![Get-MgGroup Output](get-mggroup.png)
![New-MgUser Output](new-mguser.png)
![Disable User Output](disable-user.png)
