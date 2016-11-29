#Install Windows Subsystem for Linux (or Bash on Windows)
1. Open a Powershell window

    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
    cd c:\windows\system32
    
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\AppModelUnlock" /t REG_DWORD /f /v "AllowDevelopmentWithoutDevLicense" /d "1"
    
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\AppModelUnlock" /t REG_DWORD /f /v "AllowAllTrustedApps" /d "1"
    
3. Re-start PC
4. Type 'bash' in a Windows command prompt

Once you have bash installed, run these commands

    $ sudo apt-get update && sudo apt-get upgrade

**Developer Mode Reference** https://msdn.microsoft.com/windows/uwp/get-started/enable-your-device-for-development
**WSL Reference** https://msdn.microsoft.com/en-us/commandline/wsl/install_guide

If you made a mistake and want a do-over

    PS > lxrun /uninstall /full
    PS > lxrun /install

**FAQ** https://msdn.microsoft.com/en-us/commandline/wsl/faq

##Install the Azure CLI
*Nodejs is required to run the Azure CLI*

    $ curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
      sudo apt-get install -y nodejs
     
    $ sudo npm install -g azure-cli

**Reference** https://docs.microsoft.com/en-us/azure/xplat-cli-install?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json

#Get Docker for Windows
Check this link to check the pre-reqs to run Docker on Windows https://docs.docker.com/docker-for-windows/#what-to-know-before-you-install

1. Enable Hyper-V

    PS > Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
    
2. Download Docker for Windows https://docs.docker.com/docker-for-windows/

