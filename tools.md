#install windows subsystem for linux or bash on windows
1. Enable Windows Subsystem for Linux in Programs->Features (Windows 10 Anniversary Update build 14393 or later)
   PS > Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
2. Turn on "Developer Mode" in Settings-> For developers -> Developer Mode
3. Re-start PC
4. Run 'bash' on a command prompt

*Reference* https://msdn.microsoft.com/en-us/commandline/wsl/install_guide

If you changed your mind and you want to uninstall/remove WSL
    c:\> lxrun /uninstall /full
