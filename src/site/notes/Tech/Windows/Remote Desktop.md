---
{"dg-publish":true,"permalink":"/tech/windows/remote-desktop/"}
---


# Enable Remote Desktop via [[Tech/Programming/Powershell/PowerShell\|PowerShell]]

```powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
```

This can even be done If you are remoted into a machine via PSRemoting (Enter-PSsession) as an admin.
