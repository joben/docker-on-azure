#Install Windows Subsystem for Linux (or Bash on Windows)
1. Enable Windows Subsystem for Linux in Programs->Features (Windows 10 Anniversary Update build 14393 or later)

    PS > Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
    
2. Turn on "Developer Mode" in Settings-> For developers -> Developer Mode
3. Re-start PC
4. Run 'bash' on a command prompt

Once you have bash installed, run your first command

    $ sudo apt-get update && sudo apt-get upgrade

**Reference** https://msdn.microsoft.com/en-us/commandline/wsl/install_guide

If you made a mistake and want a do-over

    PS > lxrun /uninstall /full
    PS > lxrun /install

**FAQ** https://msdn.microsoft.com/en-us/commandline/wsl/faq
