# Installing WSL2 on Windows 10
This is a short condensed setup of WSL on Windows 10. A good portion comes from https://docs.microsoft.com/en-us/windows/wsl/install-win10 with some added customizations for a more 'Linuxy' feel.

## Enable Linux via Powershell (Run as Administrator):
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

## Enable Virtual Machine Features (and Restart):
```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all

```

## Install WSL1 from the store and then click install:
Note: Currently you can only install WSL1 and then upgrade to WSL2 unless you are a Windows Insider.

Link to click (will open Microsoft Store):
https://aka.ms/wslstore


## Download and Run Kernel Update Package
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

## Upgrade the Version of the Distro
In powershell running as administrator:
```
PS C:\WINDOWS\system32> wsl --list --verbose
  NAME      STATE           VERSION
* Ubuntu    Stopped         1
```
```
PS C:\WINDOWS\system32> wsl --set-version Ubuntu 2
Conversion in progress, this may take a few minutes...
For information on key differences with WSL 2 please visit https://aka.ms/wsl2
Conversion complete.
```

## Set WSL 2 as default:
```
wsl --set-default-version 2
```

## Download and Install Ubuntu Fonts
This can be done by clicking on the fonts

## Change Colors on Terminal:
- Download ttf files from here: https://design.ubuntu.com/font/
- Double click in each ttf and click install
- Right click on top bar of ubuntu window, go to properties, and click font and select: Ubuntu Mono
- Go back to the color tab and set the 12 colors to:
```
Slot 1: Red: 48, Green: 10, Blue: 36
Slot 2: Red: 52, Green: 101, Blue: 164
Slot 3: Red: 78, Green: 154, Blue: 6
Slot 4: Red: 6, Green: 152, Blue: 154
Slot 5: Red: 204, Green: 0, Blue: 0
Slot 6: Red: 117, Green: 80, Blue: 123
Slot 7: Red: 196, Green: 160, Blue: 0
Slot 8: Red: 211, Green: 215, Blue: 207
Slot 9: Red: 85, Green: 87, Blue: 83
Slot 10: Red: 114, Green: 159, Blue: 207
Slot 11: Red: 138, Green: 226, Blue: 52
Slot 12: Red: 52, Green: 226, Blue: 226
Slot 13: Red: 239, Green: 41, Blue: 41
Slot 14: Red: 173, Green: 127, Blue: 168
Slot 15: Red: 252, Green: 233, Blue: 79
Slot 16: Red: 238, Green: 238, Blue: 238
```
- Background Color Should be Slot 1

Close out window and reopen, and setup will be complete.

## Enable Copy/Paste:
Right click on top bar of ubuntu window, go to defaults, in the Options tab check 'Use Ctrl+Shift+C/V as Copy/Paste'

## Set up links to Documents and Downloads:
```
cd ~/
ln -s "/mnt/c/Documents and Settings/<windows user>/Documents" Documents
ln -s "/mnt/c/Documents and Settings/<windows user>/Downloads" Downloads
```

## To Fix Git Hub Issues:
```
sudo umount /mnt/c
sudo mount -t drvfs C: /mnt/c -o metadata
```

## Edit to add: /etc/wsl.conf (may need to use sudo):
```
[automount]
options = "metadata"
```

## Enable scrolling in VIM (may need to use sudo):
Edit /etc/vim/vimrc.local:
```
set mouse=a
map <ScrollWheelUp> <C-Y>
map <ScrollWheelDown> <C-E>
```

## Remove Annoying Bell
Edit: ~/.bashrc:
```
bind 'set bell-style none'
```

# Enable VS Code
For VSCode, download from: https://code.visualstudio.com/

After it has downloaded, go into the ubuntu window and type 'code .' and a remote server connection will be created. Now you can create linux files / binaries within vscode.
