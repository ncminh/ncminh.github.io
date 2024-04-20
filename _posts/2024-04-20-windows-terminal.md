---
layout: post
title: Windows Terminal + Format
---
# Windows Terminal Notes

(Credit : https://gist.github.com/dahlsailrunner/ec99e195b2a4903748a74df64a1f1a94)

## Installing
* Chocolatey: `choco install microsoft-windows-terminal`
* Windows Store: https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab

**TIP:** Pin the Terminal to your Taskbar for quick and easy access

## Docs
Great docs here: https://docs.microsoft.com/en-us/windows/terminal/

## Access Settings 
Use the drop-down menu, or the `Ctrl-,` shortcut.  Recommend VS Code or Notepad++ for editor.

## Add a font
Recommendation: MesloLGS NS, but other code-oriented fonts probably also work great.
https://github.com/romkatv/powerlevel10k#manual-font-installation 

1. Just download and open / install each ttf file.

2. Then set the "fontFace" property in ***each "profile"*** in the Settings
```
{
    // Make changes here to the powershell.exe profile.
    "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
    "name": "Windows PowerShell",
    "fontFace": "MesloLGS NF",
    "commandline": "powershell.exe",
    "hidden": false,
},
```
3. Save the Settings.

## Use a Color Scheme
Some included color schemes are avaialble upon install: https://docs.microsoft.com/en-us/windows/terminal/customize-settings/color-schemes#included-color-schemes
For those schemes, you don't need to add the JSON for the scheme described in Step 2 below.

Lots of examples with screenshots and color values shown here: https://iterm2colorschemes.com/

Find JSON for the color schemes here: 
https://github.com/mbadolato/iTerm2-Color-Schemes/tree/master/windowsterminal

To use a color scheme:
1. Open `Settings` for Windows Terminal (Settings menu or `Ctrl-,`)
2. Add the JSON for any color schemes you might want to use in the `"schemes"` array. 
```json 
"schemes": [
{
  "name": "Cobalt2",
  "black": "#000000",
  "red": "#ff0000",
  "green": "#38de21",
  "yellow": "#ffe50a",
  "blue": "#1460d2",
  "purple": "#ff005d",
  "cyan": "#00bbbb",
  "white": "#bbbbbb",
  "brightBlack": "#555555",
  "brightRed": "#f40e17",
  "brightGreen": "#3bd01d",
  "brightYellow": "#edc809",
  "brightBlue": "#5555ff",
  "brightPurple": "#ff55ff",
  "brightCyan": "#6ae3fa",
  "brightWhite": "#ffffff",
  "background": "#132738",
  "foreground": "#ffffff"
}
```
3. Reference the name of the scheme as the `"colorScheme"` for the profile you want:
```json
{
    "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
    "name": "Windows PowerShell",
    "commandline": "powershell.exe",
    "fontFace": "MesloLGS NF",
    "padding": "20, 8, 8, 8",
    "fontSize": 11,
    "hidden": false,
    "colorScheme": "Cobalt2"
},
```
4. Save the `Settings` file.

## Customizing PowerShell
Run this command from a PowerShell prompt:
`Test-Path $PROFILE`

If it returns `False`, do this:
`New-Item -Type File -Force $PROFILE`

Then edit the profile
`notepad $PROFILE`

ALSO:  From an elevated (administrator) Terminal window:
```ps1
Set-ExecutionPolicy -Scope LocalMachine -ExecutionPolicy RemoteSigned
Install-Module posh-git -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
```

## Example PowerShell Profile
You will see the `PowerLevel10k-Classic` theme mentioned here -- options explained below.

```ps1
##---------------------------------------
## Theming
##---------------------------------------
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme PowerLevel10k-Classic

New-Alias npp "C:\Program Files (x86)\Notepad++\Notepad++.exe"

```
***IMPORTANT NOTE!!*** If you get an error like "Set-Theme is not valid..." then you are using a newer version of oh-my-posh.  The `Set-Theme` line should be changed to:

```
Set-PoshPrompt -Theme powerlevel10k_classic
```
To get a list of all available themes (and see example prompts!!) use the following command:

```
Get-PoshThemes
```
Pick whichever one you like for `Set-PoshPrompt` but omit the `.omp` extension.

## PowerShell Theming Options
List of available Themes here:  https://github.com/JanDeDobbeleer/oh-my-posh/tree/master/Themes
Use the filename MINUS the `.ps1` as the arg to `Set-Theme` above in the example profile.

You can see **some** of the themes shown in images/screenshots here: https://github.com/JanDeDobbeleer/oh-my-posh#themes
