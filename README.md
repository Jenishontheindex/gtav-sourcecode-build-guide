<!-- Made with ❤️ by Smashtika(@yungDoom) -->

![Icon](/other/design/icon/icon.png)

<h1 align=center>📜 --> GTA V Source Code Build Guide <-- 📜</h1>

⚠️ *If you having any problem, let us know in the ["Issues"](https://github.com/P0L3NARUBA/gtav-sourcecode-build-guide/issues) section of this repository!*<br>
💬 *You can check out ["Discussions"](https://github.com/P0L3NARUBA/gtav-sourcecode-build-guide/discussions) for talking and discuss.*

Most of this guide is from <a href="https://github.com/RockstarAdvancedGameEngine/gtav-sourcecode-build-guide">this repo</a> but I fixed some errors like missing variables and more simple directories.
I decided to make this because I spent way too much time figuring out how to fix most the issues.

# Contents
1. [Prerequisites](#prerequisites)
   1. [Base](#base)
   2. [Dependencies](#dependencies)
   3. [Miscellaneous](#miscellaneous)
   4. [Prebuilt Files](#prebuilt-files)
2. [Prerequisites Setup](#prerequisites-setup)
3. [Patching The Source Code](#patching-the-source-code)
4. [Building the files](#building-the-files)
   1. [Building The Game Binary/Executable](#building-the-game-binaryexecutable)
   2. [Building Shaders](#building-shaders)
   3. [Building Game Scripts](#building-game-scripts)
5. [Patching Game Assets](#patching-game-assets)
   1. [Main Game Assets](#main-game-assets)
   2. [Modifying the RPF Files](#modifying-the-rpf-files)
10. [Running The Game](#running-the-game)
11. [BankRelease & Debug Controls](#bankrelease--debug-controls)
12. [Working Status of the Tools and Game](#working-status)
13. [Known Issues, bugs and errors](#known-bugs-and-errors)
14. [Troubleshooting](#troubleshooting)
15. [Final Thoughts](#final-thoughts)


## Prerequisites
### Base
 - Windows 10/11 ## VM HIGHLY RECOMMENDED
    - [LTSC 2021](https://archive.org/download/Windows10EnterpriseLTSC202164Bit/en-us_windows_10_enterprise_ltsc_2021_x64_dvd_d289cf96.iso) Recommended, but you can use Normal Windows 10/11 too.
 - Latest Grand Theft Auto V Files from Steam, Epic Games or maybe Rockstar Games Launcher. 
 - Minimum 65GB Free Space, 140GB+ is Recommended because of the game files and programs.
 - GTAVSP.7z - Source Code<br>
    - **Download Link: [All Available Download Links](/source-code-links.md)**
    - Archive Password: `Mi76#b>9mRed`
   - You can verify the authenticity of the file by its SHA1 hash: `ca39323730ed644fa534a2946506d4287f92a799`
     - To verify with 7-Zip, right-click the file and select `7-Zip > CRC SHA > SHA1`
 - [update.rpf and update2.rpf from GTA V build 2699](https://mega.nz/file/72plXYpY#B9A3vDidqPUVhfXDP5hWCS8lc90lcdGZsGfjuWkBDe8)
 - Some Patience and Technical Competence

### Dependencies
 - [Visual Studio 2012](https://files.dog/MSDN/Visual%20Studio%202012/en_visual_studio_ultimate_2012_x86_dvd_2262106.iso)
    - [Update 4 for Visual Studio 2012](https://files.dog/MSDN/Visual%20Studio%202012%20Update%204/mu_visual_studio_2012_update_4_x86_dvd_3161759.iso)
- Do not download VS 2010 or update 4 if you are using VS 2022 with patches (UNRECOMMENDED) **[Visual Studio 2022 Patches](#miscellaneous)**
- (OPTIONAL) [Visual Studio 2022](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&channel=Release&version=VS2022&source=VSLandingPage&cid=2030&passive=false)
  	- Same goes here, only download if you are using the 2022 patches
 - [DirectX SDK June 2010](https://download.microsoft.com/download/A/E/7/AE743F1F-632B-4809-87A9-AA1BB3458E31/DXSDK_Jun10.exe)
 - (OPTIONAL) [3D Studio Max 2010 SDK](https://archive.org/details/sdk-3ds-max-2010)
 - [Incredibuild 4.0](https://xoreax-incredibuild.software.informer.com/4.0/)
    - This is only needed for Compiling Shaders and Game Scripts.
 - [7-Zip](https://7-zip.org/a/7z2301-x64.exe)
    - For extracting the archives.
 - [OpenIV](https://openiv.com/WebIV/guest.php?get=1)
    - For editing the game files.
 - [Git](https://git-scm.com/)
    - For Applying some patches.
 - [Perf Force P4](https://www.perforce.com/products/helix-core/free-version-control)

### Miscellaneous
 - [Rush Patches](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/files/14641602/rush_patches-master.zip)
 - [DLL Patches](https://github.com/P0L3NARUBA/gtav-sourcecode-build-guide/files/14965810/dll_patches_x.zip)
 - (OPTIONAL) [3rdParty Folder](https://mega.nz/file/SqojFJZL#eYINo1pnspuTvdbocz4cA7NYZA8BN2H2nm7YEXuzlFw)
 - (OPTIONAL) [gIKgDXuVHNzIgXkiwpB.zip - Art Asset Leak](https://big.fileditchnew.ch/b9/gIKgDXuVHNzIgXkiwpB.zip) ## Link Dead
    - [Mirror Link](https://www.bojarcz.uk/gIKgDXuVHNzIgXkiwpB.zip), Thanks to [@RockstarAdvancedGameEngine](https://github.com/RockstarAdvancedGameEngine). ## Link Dead
    - ## You can probably find a download for it on the internet archive or search up gIKgDXuVHNzIgXkiwpB.zip on 'onionized' duck duck go
 - (OPTIONAL) [Network Fix](https://github.com/Vasik96/gtav-sourcecode-build-guide/raw/main/Network.Fix.zip)
    - This will fix the Studio or IP-related issues.
    - Thanks [@Vasik96](https://github.com/Vasik96) for new download
 - [Mixed Patches](https://github.com/Vasik96/gtav-sourcecode-build-guide/raw/main/Mixed_Patches.zip)
   - Thanks [@Vasik96](https://github.com/Vasik96) for new download
 - (OPTIONAL & NOT STABLE) [Visual Studio 2022 Patches](https://small.fileditchstuff.me/s10/VBlSfKBylNQplMIPLL.zip)
    - Presented by [@userTermzik](https://github.com/userTermzik), but I don't recommend this because it needs some modifications. 

### Prebuilt Files
 - [Shaders](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/files/14649717/common.zip) ([You can build your own shaders and play with them without any problem.](#building-shaders)) ## Link Dead
 - [Game Scripts](https://drive.google.com/file/d/1AVMC_MBPpqKp0BIrOI-_lLq98QmwRn46/view) (You can still use the included game scripts from the update and update2.rpf files or )[build it yourself](#building-game-scripts)
 - [BankRelease EXE](https://drive.google.com/file/d/17Zkmoc_9RIJZNwKQyC5YWLJgf64TLuHQ/view?usp=sharing) (If you want to skip the "Building The Game Binary/Executable" step)

___

> [!NOTE]
> It is recommended to create a virtual machine for this build process, Although the build process can be done on your Real PC<br>
> It's not recommended on your Real PC because sometimes the conflicts may happen and broke the whole compilation process<br>
> **VMWare/Hyper-V are recommended to run the Virtual Machine due to their performance.**

## Prerequisites Setup
1. Install DirectX SDK June 2010
   - **If you get error S1023, Uninstall `Visual C++ 2010 Redistributable` & Reinstall DirectX SDK - (June 2010).**
2. Install 7-Zip/Win-rar
3. Install Visual Studio 2012
   - Uncheck all optional components in the installer **except "Microsoft Foundation Classes for C++"** to save space, none of them are needed for the build.
4. Install Update 4 for Visual Studio 2012
5. Install Incredibuild 4.0 (Only needed for compiling shaders and game scripts)
   - If you encounter the error that the installer is "Blocked by your administrator", follow these steps:
      1. Hold Shift and right click the `incredibuild4_0.exe` file, select "Copy as path"
      2. Open Command Prompt as Administrator
      3. Paste the path and press Enter
   - Select to install "Incredibuild Agent", "Incredibuild Coordinator", and the extension for Visual Studio
6. Install OpenIV
7. Extract [DLL Patches and Rush Patches](#miscellaneous)
8. (OPTIONAL) Install 3D Studio Max 2010 SDK
9. Create X:\ Drive by following the steps at the bottom:
    1. Open Command Prompt
    2. Create a new folder called "GTA" to the Desktop or anywhere that you want
    3. Run `net use X: \\localhost\c$\<Path to working folder for build> /persistent:yes`
       - Example: `net use X: \\localhost\c$\Users\<username>\Desktop\GTA /persistent:yes`
10. Create the folder `X:\gta5` and copy all folders from `GTAVSP.7z\GTA V Source` into it
11. Right click the folder `X:\gta5`, select "Properties", uncheck "Read-only", click Apply then OK
12. Open Command Prompt as Administrator and run the following commands, then close:
```batch
setx /m RS_TOOLSROOT X:\gta5\tools_ng
setx /m DXSDK_DIR "C:\Program Files (x86)\Microsoft DirectX SDK (June 2010)"
setx /m RS_CODEBRANCH X:\gta5\src\dev_ng
setx /m RS_PROJECT gta5
setx /m RAGE_DIR X:\gta5\src\dev_ng\rage
```
13. (OPTIONAL) Symlink the `X:\gta5\titleupdate\dev_ng` directory.
    - This can be done with this CMD Command: `mklink /D /J "X:\gta5\titleupdate\dev_ng" "INSERT_RETAIL_COPY_HERE"`.
      **(``INSERT_RETAIL_COPY_HERE`` being your GTA V Game Directory)**
14. If you dont want to symlink, Put all the game files to the `X:\gta5\titleupdate\dev_ng` directory.
15. To ensure changes are finalized, restart build machine/computer.

## Patching The Source Code
1. Open `rush_patches-master.zip`
2. Copy `game` and `rage` folders to `X:\gta5\src\dev_ng`, make sure to overwrite when copying
3. (OPTIONAL) To skip launcher requirement for running the game, copy `game` and `rage` folders from `rush_patches-master.zip\OPTIONAL_FIXES` to the same folder
4. Copy all folders in `dll_patches_x.zip` to `X:\gta5\tools_ng\bin`, make sure to overwrite when copying
5. (OPTIONAL) Extract `Network Fix.zip` and put the 2 files into `x:\gta5\tools_ng\etc\globals`, make sure to overite all files when copying
7. (OPTIONAL) Install 3rdParty Folder, Extract and Put the folder to `X:\gta5\`.
8. Install Mixed Patches using git
   1. Extract everything from `Mixed_Patches.zip` to `X:\gta5\stc\dev_ng`
   2. Launch `auto.bat` then wait for the file to patch the source
   3. Close the cmd window

**By far, Your Folder Structure should look like this:**
```
🖥️ X:
 ┗ 📂 gta5
    ┣ 📂 3rdParty - (OPTIONAL)
    ┣ 📂 src
    ┃ ┣ 📂 dev_ng
    ┣ 📂 script
    ┃ ┣ 📂 dev_ng 
    ┗ 📂 tools_ng
```
## Building The Files

#### Building The Game Binary/Executable
>## Game Directory
`x:\gta5\title_update\dev_ng`

1. Run `X:\gta5\src\dev_ng\game\VS_Project\load_sln_unity_2012.bat`
	- If prompted with "How do you want to open this file?", check "Always use this app to open .sln files" and Select **Visual Studio 2012** then click OK
2. Once the solution loads, open the dropdown menu that says "Debug" at the top, select "Configuration Manager"
3. Change "Active Solution Platform" to "x64" and close the configuration window
4. Hold Ctrl key and click all projects under "GameLibs" and "Rage" folder, right-click and select "Properties"
5. In the "Configuration" dropdown, select "All Configurations"
6. Select `C/C++ > All options`, under "Look for options or switches", search "err" and set "Treat Warnings as Errors" to "No (/WX-)", then click "Apply" and "OK"
   - For faster compiles, search "mul" and set "Multiprocessor Compilation" to "Yes (/MP)"
      - If you get the error `C1060: Compiler is out of heap space` during build, come back to the above setting and turn it off
7. Right-click the "game" project and select "Properties" and do step 5,6 again
8. Change build the type at the top of the window from "Debug" to "BankRelease"
10. At the top of the window, select `Build > Build Solution` and wait for build to finish
11. Copy output binary to game folder.

> [!WARNING]
> Building shaders and game scripts can be skipped using the [prebuilt files above](#prebuilt-files)<br>
> For shaders, Extract `common.zip` and put the `common` folder into your [Game Directory](#game-directory)<br>
> For scripts, Run OpenIV and put the `script.rpf` file into `x:\gta5\title_update\dev_ng\update\update2.rpf\x64\levels\gta5\script`<br>
> These steps are here to allow modding or for those who prefer to build from source as much as possible<br>

## Setting Another System Variable
Right-click This PC > Properties > Advanced system settings > Environment Variables.
Under User variables, click New.
Variable Name: RAGE_DIR
Set Path to X:\gta5\src\dev_ng\rage
Repeat for System Variable

### Building Shaders
1. hold control and click shaders_rc and shaders_dependency then right click and properties
2. Go to VC++, then click Include directories'dropdown menu and click <edit>
3. In the top box (User-Specified Values), add $(Inherit);$(RAGE_DIR)\base\src
4. Now click ok, apply, ok and close out the properties
5. Under "Shaders", right click the "shaders_rc" project and click "Build"
6. (OPTIONAL) Build low quality shaders
   1. Right click the "shaders_rc" project and click "Properties"
   2. Select `Configuration Properties > NMake`
   3. Under "General", change all command lines from ending with `win32_40.bat` to ending with `win32_40_lq.bat`, then click "Apply" and "OK"
   4. Rebuild shaders and wait it to finish
This will take a while
7. title_update is your game directory automatically so visual studio will build there, if the "common" folder isn't in the directory repeat step 5 (and 6 if you build lq shaders).

### Building Game Scripts
1. Open Command Prompt and Run the following commands:
```batch
X:
cd X:\gta5\src\dev_ng
setenv
cd ..\..\tools_ng\bin\RageScriptEditor
ragScriptEditor
```
3. In the editor, select `File > Open Project` and open `X:\gta5\script\dev_ng\singleplayer\GTA5_SP.scproj`
4. Select `Compiling > Intellibuild > Build Project` and wait until the compiling process finishes.
5. Run OpenIV, select "Windows" under "Grand Theft Auto V"
6. Select the game folder and click "Continue"
7. Open `<Game Directory>\update\update2.rpf\x64\levels\gta5\script`
8. Delete `script.rpf`
9. Click the "Edit mode" button, and copy `X:\gta5\titleupdate\dev_ng\x64\levels\gta5\script\script.rpf` to the OpenIV window.


## Patching Game Assets
#### Main Game Assets

1. Install ``update.rpf and update2.rpf from GTA V build 2699`` from [Prerequisites List](#prerequisites)
2. Put `update.rpf` and `update2.rpf` files to `<Game Directory>\update\` folder
   * **Dont forget to backup your old files from update folder.**

#### Modifying the RPF Files
If you ever modify the RPF files, dont forget to encrpyt them.<br>
**Here you can see how to do it:**
1. From `rush_patches-master.zip`, copy all files in the `ARCHIVEFIX` folder to a separate location
2. Drag RPF file(s) onto `ArchiveFix.exe`
   * Don't drag the both files at the same time, **just drag one by one**.


## Installing Prebuilt Stuff
##### Prebuilt Shaders
1. Go to game directory
2. Put the `common` folder to the game directory.
##### Prebuilt Game Scripts
* Scripts Already included in update2.rpf, you can replace it in future with one that you builded it.
#### Prebuilt Binary
Copy the game-win64-bankrelease.exe file from [Prebuilt Files](#prebuilt-files) and paste it into the game directory (
```batch
X:\gta5\titleupdate\dev_ng\
```
)

## Running The Game
1. Rename the original `GTA5.exe` to `LGTA5.exe` and change the prebuilt/compiled binary file from `game-win64-bankrelease.exe` to `GTA5.exe`
2. In the game directory, create a file named `launch.bat` and add these contents:
```batch
cd %~dp0
GTA5.exe -noSocialClub -nokeyboardhook -nonetlogs
```
2. (OPTIONAL) Add additional arguments:
 - `-kbgame` - Start game with game keyboard enabled
 - `-output` - Show console log of game, the game opens a little bit slow.
 - `-rag` - Enable support for RAG, the internal game debugging tool
    - `-ragUseOwnWindow` - Use it with `-rag` parameter to make game run outside of RAG Render Window
    - **DO NOT** Forget to Launch RAG Before launching the game if u using any RAG parameters
 - `-DoReleaseStartup` - Start real Story Mode on launch, Ignore if it says unknown parameter/command
    - If you dont type this parameter, you will spawned in a random location as a random character with a random clothes
 - Additional standard game arguments can be added as well.
   - [Here is the almost all the arguments list](other/LAUNCHPARAMS_GTAV.txt) 
3. (OPTIONAL) Launch RAG with the following commands in Command Prompt:
```batch
X:
cd X:\gta5\src\dev_ng
setenv
cd ..\..\tools_ng\bin\rag
rag
```
4. Run `launch.bat`

## BankRelease & Debug Controls

[Almost Every Controls & Keys](/other/controls)

## Working Status

## Compiling
- [x] Can Compile Game
- [x] Can Compile Tools
- [x] Can Compile Game Scripts
- [x] Can Compile Shaders

## Main
- [x] Game
  - [ ] Script Hook V and ASI Loaders
- [x] Tools
  - [x] Rage Script Editor
  - [x] Rag
    - [x] Rag UI
    - [x] Rag Interface 
  - [x] Map Viewer
  - [x] Shortcut Menu 
  - [x] Other Tools
    - Note that Some Perforce login required tools will not work, they need some modifications and Perforce.
      - Perforce Download Links:
        1. Helix Core: https://www.perforce.com/downloads/helix-core-free-small-teams
        2. Helix Visual Client: https://www.perforce.com/downloads/helix-visual-client-p4v

## Known Bugs and Errors

> B = Bug - E = Error - F = Fix

**B:** When I create "Vehicles" Widgets, the game crashes.<br>
**F:** Before Opening The Save Game, just enter the game normally and dont load the save, create vehicle widgets then load the game.

**E:** Fatal Error: Unable to create default effect 'common:/shaders/im', cannot continue.<br>
**F:** If u didn't put the shaders to the game directory or you dont have the low quality shaders, then this error may appear.

#### Solution 1: 
Just Simply Put the shaders to the game directory and compile the low quality shaders by following tutorial.

#### Solution 2:
Just make your shaders quality "High" and dont lower that.<br>
To do this, Follow this steps:

1. Go To **\Documents\Rockstar Games\GTA V**
2. Open *settings.xml*
3. Change  `<ShaderQuality value="0" />` To `<ShaderQuality value="1" />`
4. Save the file and Done!

**E:** Couldn't connect to RAG.exe. Keep trying?<br>
**F:** Just Simply Open the RAG Manually, then start **launch.bat**.

**E:** Fatal Error: Fatal disc error (code -*)<br>
**F:** You are %100 missing some files or misdragged something, fix your game files.

# Known Issues
* Game crashes if you open "Keybinds" Menu in BankRelease or Debug Builds.
  * It's because the game tries to load a missing keyboard layout file.
    * This can probably be fixed by just editing some lines in the source code.
   
## Credits
- [@GTA-Source-Helper](https://github.com/GTA-Source-Helper)
   - Network Fix
- [@RockstarAdvancedGameEngine](https://github.com/RockstarAdvancedGameEngine)
   - OneDrive Link for Source Code
   - Mirror Link for Art Asset Leak
-[@voyageprofessor](https://github.com/voyageprofessor)
  - Prebuilt Game Scripts
- Other Contributors / Supporters
   - Thanks to all of you guys!
  


