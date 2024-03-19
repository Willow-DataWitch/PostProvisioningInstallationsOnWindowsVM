# After you create your windows server

... and throw some default image on it, you need OTHER THINGS.

USEFUL THINGS.

So I connect at the command line (go see https://github.com/Willow-DataWitch/terraform-an-azure-devbox/tree/main/PowerShellRemotingServer for spinning a Windows VM and configuring it for remote commandline access in the Azure cloud with terraform) and run something like this:

```powershell
#region Get a package manager.
Write-Verbose -Verbose "Installing the chocolatey package manager...";
<#from https://chocolatey.org/install#install-step2 #> Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1')); 
Write-Verbose -Verbose "Refreshing the environment to enable chocolatey...";
Import-Module $env:ChocolateyInstall\helpers\chocolateyProfile.psm1;
refreshenv;
#endregion Get a package manager.

#region Install stuff.
Write-Verbose -Verbose "Installing Visual Studio Code...";
choco install vscode -y;
#endregion Install stuff.

Write-Verbose -Verbose "Refreshing the environment to enable all your newly installed packages...";
refreshenv;
```

## Package Manager
I like chocolatey for this.
