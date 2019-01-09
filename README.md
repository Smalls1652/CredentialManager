# Credential Manager for Windows' PasswordVault

There are numerous ways to save credentials in PowerShell, but the only two that are considered remotely secure are:

1. Certificate-based authentication
2. Windows' PasswordVault

This module attempts to be a way for you to store your credentials for authentication to servers, machines, or anything else requiring username & password based authentication. There are numerous implementations of PasswordVault in PowerShell, but this is my implementation of how I wanted it to work.

I actually have not utilized anyone else's code for my own personal use (Meaning I have never downloaded anyone else's module), so I'm not sure how they do it. The way I do it, is to be as secure as possible. Instead of getting, storing, and removing passwords in your current PowerShell session, a background job is opened and closed to process data. Anytime a password is returned to your session, it is returned as a PSCredential object. You can then pass that object to any credential parameter in another command or as a variable.

## Requirements

* Windows 10
* PowerShell 5 (**Not PowerShell Core as far as I am aware!**)

## Installation

The easiest way to install this is by using `git clone`:

```powershell
Set-Location -Path ~\Documents\WindowsPowerShell\Modules\
git clone https://github.com/Smalls1652/CredentialManager
```
Restart your PowerShell console and you'll be able to utilize this module.

## Usage

Here are the help files for the three commands:

### New-VaultCredential

```powershell
<#
.SYNOPSIS
Creates a new credential in Windows' PasswordVault.

.DESCRIPTION
Creates a new credential in Windows' PasswordVault for secure storage.

.PARAMETER Resource
The name of the resource you want to save the credential under.

.PARAMETER Credential
Pass a PSCredential object.

.EXAMPLE
New-VaultCredential -Resource "Service Account" -Credential (Get-Credential)

.NOTES
The purpose of saving your credentials to the PasswordVault is that it's a more secure storage system compared to saving credentials to the local disk. Certificate-based authentication is still a more preferred method, but this is a secondary alternative.
#>
```

### Remove-VaultCredential

```powershell
<#
.SYNOPSIS
Remove items from Windows' PasswordVault.

.DESCRIPTION
Remove items from Windows' PasswordVault. Asks to remove the item before removal.

.PARAMETER Resource
The resource that you want to delete items from.

.EXAMPLE
Remove-VaultCredential -Resource "Service Accounts"

.NOTES
The purpose of saving your credentials to the PasswordVault is that it's a more secure storage system compared to saving credentials to the local disk. Certificate-based authentication is still a more preferred method, but this is a secondary alternative.
#>
```

### Get-VaultCredential

```powershell
<#
.SYNOPSIS
Get an item from Windows' PasswordVault.

.DESCRIPTION
Get an item from Windows' PasswordVault.

.PARAMETER Resource
The resource that you want to get an item from.

.PARAMETER UserName
If more than one UserName is stored under a resource, use this to specify a UserName.

.EXAMPLE
Get-VaultCredential -Resource "Service Accounts" -UserName "example\jldoe123"

.NOTES
The purpose of saving your credentials to the PasswordVault is that it's a more secure storage system compared to saving credentials to the local disk. Certificate-based authentication is still a more preferred method, but this is a secondary alternative.
#>
```