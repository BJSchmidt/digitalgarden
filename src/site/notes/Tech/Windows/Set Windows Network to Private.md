---
{"dg-publish":true,"permalink":"/tech/windows/set-windows-network-to-private/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# Set Windows Network Category to Private

Open an elevated [[Tech/Programming/Powershell/PowerShell|PowerShell]] session

Get current profiles. Make sure you are logged on to the network you want to change.

``` Powershell
Get-NetConnectionProfile
```

Change the network in your list to be Private

``` Powershell
Set-NetConnectionProfile -Name "MYNETWORK" -NetworkCategory Private
```

Check that everything went fine

``` PowerShell
Get-NetConnectionProfile
```
