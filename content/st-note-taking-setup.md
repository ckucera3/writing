+++
date = "2016-05-14T14:56:44-04:00"
draft = true
title = "Sublime Text Note Taking Set up for Windows"

+++

I have long searched for a note taking tool that is discrete, highly customizable, easy to toggle on/off, markdown compatible, and able to sync across devices. Eventually I settled for using the text editor Sublime Text 3, Dropbox and an AutoHotKey script. In this post, I'll take you through the setup step-by-step.

Follow this guide if you want a note taking tool that:

- allows keybindings to minimize/maximize the tool
- is Markdown compatible (including MathJax)
- can export to PDF and HTML
- has adjustable transparency
- can be backed up on the cloud and used across multiple devices
- can be made to 'stick' to the top of a page


<video src="/writing/vid/note-taking-example-1.mp4" autoplay muted loop />

> My note taking set up

**NOTE: This is a set up for windows, specifically Windows 10. It might not work for older Windows versions. For Mac and Linux users, I don't know of an alternative to AutoHotKey, so this set up will not work for you.**

## Sublime Text 3

It's a nice text editor. If you haven't used it before, I recommend trying it out. It is fast when dealing with huge files and is very customizable with its popular [package ecosystem](https://packagecontrol.io/). Other features include multiple cursors, very useful selection/find/replace key bindings, and a nice look. Isn't it pretty? A downside is that it isn't free or opensource. It costs money, but there's an unlimited free trial period that you can use if unable to fork over the cash. Since using this product has helped me improve my programming workflow (and has made it more enjoyable), I do plan on paying for the program once I become profitably employed out of college.

## AutoHotKey
AutoHotKey (AHK) is a scripting language for Windows that allows users to create hot-keys and text macros. It's very useful if you don't want to mess around with batch files.


## Instructions

Now, on to the setup up guide.

1. Download [ST3](https://www.sublimetext.com/)
2. Follow the [instructions](https://packagecontrol.io/installation) for installing Package Control 
3. Install the following packages
    + MarkdownEditing
    + OmniMarkupPreviewer
    + Optional, but useful, packages
        * InsertDate
        * SideBarEnhancements
4. Install [AHK](https://autohotkey.com/download/). Test it out with whatever sample script is provided to you. When AHK is running, it should also be viewable in your task pane as an H with a green background.
5. Create your script. 
Here's the AHK script I use:
    
```
/*
Hotkeys:
Windows Key + N: toggles Sublime Text window
Windows Key + space: 'sticks' window on top of other windows -OR- 'unsticks' the window
Alt-W: make window less transparent
Alt-S: make window more transparent
*/

#t:: appFlapper("cmd.exe")

#n::    appFlapper("sublime_text.exe")
appFlapper(exePath) {
    IfWinExist, % "ahk_exe " substr(exePath, instr(exePath, "\",, 0)+1)
        IfWinActive
            WinMinimize
        else
            WinActivate
    else
        Run, %exePath%
}

#InstallKeybdHook
#SingleInstance force


#space::
WinGet, currentWindow, ID, A
WinGet, ExStyle, ExStyle, ahk_id %currentWindow%
if (ExStyle & 0x8)  ; 0x8 is WS_EX_TOPMOST.
{
    Winset, AlwaysOnTop, off, ahk_id %currentWindow%
    SplashImage,, x0 y0 b fs12, OFF always on top.
    Sleep, 1500
    SplashImage, Off
}
else
{
    WinSet, AlwaysOnTop, on, ahk_id %currentWindow%
    SplashImage,,x0 y0 b fs12, ON always on top.
    Sleep, 1500
    SplashImage, Off
}
return

!w::
WinGet, currentWindow, ID, A
if not (%currentWindow%)
{
    %currentWindow% := 255
}
if (%currentWindow% != 255)
{
    %currentWindow% += 5
    WinSet, Transparent, % %currentWindow%, ahk_id %currentWindow%
}
SplashImage,,w100 x0 y0 b fs12, % %currentWindow%
SetTimer, TurnOffSI, 1000, On
Return

!s::
SplashImage, Off
WinGet, currentWindow, ID, A
if not (%currentWindow%)
{
    %currentWindow% := 255
}
if (%currentWindow% != 5)
{
    %currentWindow% -= 5
    WinSet, Transparent, % %currentWindow%, ahk_id %currentWindow%
}
SplashImage,, w100 x0 y0 b fs12, % %currentWindow%
SetTimer, TurnOffSI, 1000, On
Return


TurnOffSI:
SplashImage, off
SetTimer, TurnOffSI, 1000, Off
Return

```


After this script is up and running, the set up should be complete.