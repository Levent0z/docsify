# Tips for Switching between Windows and MacOS


<details><summary style="font-size:1.5em">Prologue</summary>
As a long-time user of Windows, I'm here to tell you that switching to a MacOS doesn't have to be painful. Had I had access to a post like this, I'm sure it would have saved me tons of time. If you've just received your first Macbook (or Windows machine) and want to get a head-start and become productive quickly, read on!
</details>

## TL;DR
Are you switching from Windows to macOS, or vice-versa? Here are some tips to hit the ground running.


### Good News - They Are More Similar Than Not
You will find that, perhaps unsurprisingly, Windows and macOS have very similar functionality in a lot of respects, but take opposite approaches in various areas. Switching from one to the other is like learning to drive in Britain when you've been driving in the US (or vice-versa). 

Let's take a high-level look at what we have in Windows and macOS.

| Function            | name in Windows             | shortcut           | name in macOS       | shortcut             |
| -                   | -                           | -                  | -                   | -                    |
| App List            | Start Menu                  | Win                | Launch Pad          | _unset by default_   |
| App Launcher        | Run Command                 | Win + R            | Spotlight Search    | Cmd + Space          |
| App Shortcuts       | Taskbar                     |                    | Dock                |                      |
| File Management     | File Explorer               | Win + E            | Finder              | _Seek via Cmd + Tab_ |
| Process Management  | Task Manager                | Ctrl + Shift + Esc | Activity Monitor    |                      |
| Configuration       | Control Panel / Settings    |                    | System Preferences  |                      |
| Console             | Command Prompt / PowerShell |                    | Terminal            |                      |
| Multiple-Desktops   | Task View                   | Win + Tab          | Mission Control     | Ctrl+Up              |
| Simple Text Editor  | Notepad                     |                    | Notes               |                      |
| Rich-Text Editor    | Wordpad                     |                    | TextEdit            |                      |
| Post-It Editor      | Sticky Notes                |                    | Stickies            |                      |
| Simple Image Editor | Paint                       |                    | _unvailable?_       |                      |
| Cloud Service       | OneDrive                    |                    | iCloud              |                      |
| Voice Assistant     | Cortana                     |                    | Siri                |                      |
| Notifications       | Notification Center         | Win + A            | Notification Center | _unset by default_   |
| Screen Capture      | Snipping Tool               |                    | Screenshot          | Cmd + Shift + 5      |
| System Logs         | Event Viewer                |                    | Console             |                      |

There are some key points that I think you should be aware of.

1. Macbook keyboards lack several keys that you might be used to from Windows-based keyboards. Don't fret, most functionality can be reproduced using a combination of keys. The most important, in my opinion, is that the `delete` key on Windows is `Fn + Backspace` on Mac. 
2. **On macOS**, right-click is achieved by tapping on the touchpad using two-fingers.
3. **On macOS**, swiping left or right using three-fingers allow you to switch to the next or previous desktop.
3. The highest-privilege user on Windows is called `Administrator`, and on the Mac it's called `Super User` or `root`.
4. Software installation experience (for non-app store applications) is quite different:
   - **On Windows**, typically there's an installer executable (e.g. `setup.exe` or `setup.msi`) which when run takes the user through multiple steps. At the end the application becomes available in the `Start Menu`. To uninstall it, use `Add or Remove Programs` functionality.
   - **On the Mac**, if there's an installer, it has a simplistic UI that expects you to drag&drop the app's icon from the left (or top) to the Applications icon on the left (or bottom). Otherwise, copying an executable into the `Applications` folder makes it available to run. To uninstall it, simply select the icon in the folder and select `Move to Trash` in the right-click menu.


## Window Management

Most applications typically have a window as their main user-interface. Windows can be positioned and resized using the mouse/touchpad or the keyboard. A window's control icons are on the top-right on Windows, and on the top-left on macOS. On Windows, each application owns its own menu area within the bounds of its window. On macOS, every application shares the top menu, which shows the menu of the currently focused application.
 
| Function                               | Key on Windows     | Key On macOS                                       |
| -------------------------------------- | ------------------ | -------------------------                        |
| Exit Application                       | Alt + F4           | Cmd + Q                                          |
| Minimize Window                        | Win + Down         | Cmd + M                                          |
| Hide Window                            |                    | Cmd + H                                          |
| Maximize Window (in current desktop)   | Win + Up           | _Use [Spectacle](https://www.spectacleapp.com/)_ |
| Full-screen App (into its own desktop) |                    | _Customize "Zoom" in Keyboard shortcuts_         |
| Show Desktop                           | Win + M            | F11                                              |
| Dock Window To Left                    | Win + Left         | _Use [Spectacle](https://www.spectacleapp.com/)_ |
| Dock Window To Right                   | Win + Right        | _Use [Spectacle](https://www.spectacleapp.com/)_ |
| Switch Between Applications            | Alt + Tab          | Cmd + Tab                                        |
| Switch Between Desktops                | Win + Tab          |                                                  |
| Screenshot Desktop                     | PrtSc              | Cmd + Shift + 3                                  |
| Screenshot Window                      | Alt + PrtSc        | Cmd + Shift + 4                                  |
| Magnifier Zoom In                      | Win + =            | _Try_ Cmd + =                                    |
| Magnifier Zoom Out                     | Win + -            | _Try_ Cmd + -                                    |
| Lock the Computer                      | Win + L            | _configurable in TouchPad_                       |

> Spectacle is a great app for the Mac that adds Windows-like docking capabilities to applications on the Mac. [Download it here](https://www.spectacleapp.com/). After you add it to Applications, it will appear on the top-right of the screen with a glasses icon. You'll want to check the `Launch Spectacle at Login` option in its preferences menu.

## Editing and Cursor Navigation

I strongly recommend spending some time memorizing and getting used to the new shortcuts for increased productivity.

| Function                               | Key on Windows     | Key On macOS              |
| -------------------------------------- | ------------------ | ------------------------- |
| Cut                                    | Ctrl + X           | Cmd + X                   |
| Copy                                   | Ctrl + C           | Cmd + C                   |
| Paste                                  | Ctrl + V           | Cmd + V                   |
| Undo                                   | Ctrl + Z           | Cmd + Z                   |
| Redo                                   | Ctrl + Y           | Cmd + Shift + Z           |
| Delete character in front of cursor    | Delete             | Fn + Delete               |
| Move cursor to beginning of line       | Home               | Cmd + Left                |
| Move cursor to end of line             | End                | Cmd + Right               |
| Move cursor to top of file             | Ctrl + Home        | Cmd + Up                  |
| Move cursor to bottom of file          | Ctrl + End         | Cmd + Down                |
| Move cursor to beginning of word       | Ctrl + Left        | Option + Left             |
| Move cursor to end of word             | Ctrl + Right       | Option + Right            |


## Getting Started with Console
If you need to run command-line tools, this section is for you. The console is called **Command Prompt** on Windows and **Terminal** macOS. These run, by default, DOS or PowerShell and Bash respectively.

| Function                         | Windows                                      | Mac                           |
| -------------------------------  | -----------------------------------------    | -------------                 |
| Folder separator character       | _backslash_ ( \\ )                           | _slash_ ( / )                 |
| Escape character for whitespace  | _Pair of double-quotes ( " ) as delimiters_  | _slash followed by the space_ |
| Print current working directory  | cd                                           | pwd                           |
| List files & folders             | dir                                          | ls                            |
| List all files & folders         | dir /ah                                      | ls -la                        |
| Change directory                 | cd _path_                                    | cd _path_                     |
| Create directory                 | md                                           | mkdir                         |
| Remove directory                 | rd _path_                                    | rmdir _path_                  |
| Remove directory recursively     | rd -r _path_                                 | rm -rf _path_                 |
| Find text in files               | findstr _keyword_                            | grep _keyword_                |
| Display contents of text file    | type _path_                                  | cat _path_                    |
| Administrator mode               | runas                                        | sudo su                       |
| Current user's home directory    | %USERPROFILE%                                | $HOME _or_ ~                  |
| Path environment variable        | %PATH$                                       | $PATH                         |
| Paths separator character        | _semi-colon_ ( ; )                           | _colon_ ( : )                 |
| Move cursor to beginning of line | _Home_                                       | _Ctrl + A_                    |
| Move cursor to end of line       | _End_                                        | _Ctrl + E_                    |
| Erase current line               | _Esc_                                        | _Ctrl + A, Ctrl + K_          |
| Clear Screen                     | cls                                          | clear _or Cmd + K_            |
| Text-based editor                |                                              | vim _or_ nano                 |



## Additional Tips
These tips are worth their weight in virtual gold.

### 1. Scroll Direction
The default scroll direction on Windows and Mac are opposite. Mac calls its default direction as "natural". Even though the direction can be changed in `System Preferences`, you may find that the mouse wheel direction and the scroll gesture using two fingers are still opposite. To resolve this issue, I have two suggestions:

1. If using a Logitech mouse, see if scroll reversing functionality is available to you in the [Logitech Options](https://support.logitech.com/en_us/software/options) app.
2. Install the free [Scroll Reverser](https://pilotmoon.com/scrollreverser/) app, which will appear in the top-right menu.


### 2. Moving the Taskbar/Dock
**On Windows**, the `Taskbar` can exist on the top, left, right or bottom of any monitor in a multi-mon setup. It can also be configured to show all apps, or just its monitor's apps. To reposition it, drag it from an empty space on the taskbar and drop it to any monitor edge. 

**On macOS**, the `Dock` can only appear on one monitor at a time, and only at the bottom, left or right. To change its position, go to `System Preferences > Dock`. To move it to another monitor, drag the pointer to the bottom edge of that monitor and the Dock will reposition itself there.


### 3. Running Executables Downloaded from the Internet
By default, both Windows and Mac tries to protect their users by blocking execution of software downloaded on the internet. To bypass this:
**On Windows**, right click the blocked executable's icon and select `Properties` from the menu. Click `Unblock` at the bottom of the `General` tab.
**On macOS**, go to `System Preferences > Security & Privacy` and click `Allow` at the bottom of the `General` tab.


### 4. Showing Hidden Files

**On Windows**, in Explorer, check `Hidden Items` in the `View` ribbon.

**On macOS**:
1. Launch `Terminal` and enter the following: 
```sh
defaults write com.apple.finder AppleShowAllFiles YES
```
2. While holding the `option` key, right-click on Finder icon on the `Dock` and select `Relaunch`.


> Did you know? On macOS, files and folders with names that begin with the dot character (.) are hidden by default.


### 5. Quitting Applications

**On macOS**, closing an app using the top-left red button on its window doesn't quit the application, unlike the top-right button on Windows. To quit the application, select `Quit` from the applications top menu, or use the `Cmd + Q` shortcut.


### 6. File Paths 

**On Windows**, you can set the path at `System Properties > Advanced > Environment Variables`.

**macOS**, the path is a composite value, which might contain values from `/etc/paths`, `/etc/profile`, `~/.bash_profile`, `~/.bash_login`, `~/.profile`. To add a path on Mac, create a file whose contents is the path as follows:
```sh
echo "/some/path/to/the/binary" >> /etc/paths.d/variable  #Replace variable with a name unique in that folder
```

> Also be aware of the existence of `/usr/libexec/path_helper` executable.

---
<details><summary style="font-size:1.5em">Disclaimer</summary>
This post is based on my personal experience on the 3rd-gen Lenovo Thinkpad X1 Carbon laptop running `Windows 10 Pro 1803` and my 2016+ MacBook Pro with TouchPad running `macOS Mojave 10.14`. The content is not meant to be complete or authoritative and I apologize for any omissions or inaccuracies.
</details>
