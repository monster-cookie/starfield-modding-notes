# Development Workflow

## Prerequisites 

I don't use the BGS Papyrus plugin because its pretty opinionated and requires working from specific directories that don't play well with GIT based development 

1) Need a public or private GIT repo
2) Need SFCK
3) Need VS Code with Papyrus Plugin (https://marketplace.visualstudio.com/items?itemName=joelday.papyrus-lang-vscode)
4) Need powershell
5) If you are not using MO2, you will need a file watcher to watch the Game Data directory and catch the random files CK makes like terrain, geomerties, etc. I recommend [FolderChangesView](https://www.nirsoft.net/utils/folder_changes_view.html)
6) Nifskope

## Repository Setup

This works best with MO2 but MO2 VFS hasn't been working well on later Win11 installs. I mean it works but causes noticible lag and some tooling like nifskope/spriggit don't play well with it. 

### MO2

Coming Soon, I need to use MO2 to sort out it compability issues with Creations Forge anyway. 

### Vortex

Generally these instructions only need done once

1) Open SFCK, make a new ESP for your creation
2) Zip the ESP and move the zip to ~/Downloads
3) Delete the original ESP if it still in the Game Data folder
4) Open Vortex install the zip as a custom mod
5) Open VS Code and option the repo
6) Copy the files in one my projects .vscode folder
7) Copy all the files from the Tools folder of one of my projects
8) Edit sharedConfig.ps1, set $Global:ScriptingNamespaceModuleCompany, $Global:ScriptingNamespaceModuleName, $Global:ScriptingNamespaceSharedLibraryCompany, $Global:ScriptingNamespaceSharedLibraryName, and $Global:Databases
9) Create a .env file (no black lines) see ENV Setup below in the References Section
10) Delete the Staging folder if it exists
11) In Powershell run ./Tools/setupRepo.ps1, this creates a folder junction with the MO2/Vortest staging folder

## Normal Workfloe

### Papyrus Scripts

1) Open VS Code
2) Make your edits
3) Run Tasks -> Run -> Compile Scripts
4) Open your GIT IDE and commit the changes

### Game Database (ESP)

If you have papyrus changes make them before launching SFCK.

1) If not using MO2, remember to launch and set to moniytoring the FolderChangesView file watcher
2) Open SFCK (If using MO2 you have to launch it from MO2)
3) Open the ESP
4) Make your changes
5) Use File -> Convert Archive (YOU MUST MATCH the ESM size type)
6) Uncheck the ESP from the load order
7) Launch Starfield and Test
8) Open your GIT IDE and commit the changes

## References

### .env file
```Plain Text
STEAM_GAME_FOLDER=C:\Steam\steamapps\common\Starfield
STEAM_DATA_FOLDER=C:\Steam\steamapps\common\Starfield\Data
#
TOOL_PATH_PAPYRUS_COMPILER=C:\Steam\steamapps\common\Starfield\Tools\Papyrus Compiler
TOOL_PATH_ARCHIVER=C:\Steam\steamapps\common\Starfield\Tools\Archive2
TOOL_PATH_XTEXCONV=C:\Modding\DDSConverter\Converters\SF
TOOL_PATH_ASSET_WATCHER=C:\Steam\steamapps\common\Starfield\Tools\AssetWatcher
TOOL_PATH_SPRIGGIT=C:\Modding\Spriggit
#
PAPYRUS_SCRIPTS_PATH=C:\Steam\steamapps\common\Starfield\Data\Scripts
PAPYRUS_SCRIPTS_SOURCE_PATH=C:\Steam\steamapps\common\Starfield\Data\Scripts\Source
PAPYRUS_COMPILER_FLAGS=C:\Steam\steamapps\common\Starfield\Data\Scripts\Source\
#
SPRIGGIT_VERSION=0.40.1
#
MODULE_DATABASE_PATH=C:\Users\monst\AppData\Roaming\Vortex\starfield\mods\Venworks - Encounters Overhaul
MODULE_SCRIPTS_PATH=C:\Users\monst\AppData\Roaming\Vortex\starfield\mods\Venworks - Encounters Overhaul\Scripts
MODULE_SCRIPTS_SOURCE_PATH=C:\Users\monst\AppData\Roaming\Vortex\starfield\mods\Venworks - Encounters Overhaul\Scripts\Source
```

NOTE: .env can't process ENV variables, go figure, so all the path must be fully qualified

- STEAM_GAME_FOLDER is the path to the Starfield game usually Steam but Gamepass/MS Store version can work too but data dir becomes complicated
- STEAM_DATA_FOLDER is the Data subdirectory of the Starfield dame directory. In Game Pass this may be ~/Documents/My Games.
- TOOL_PATH_PAPYRUS_COMPILER is the path to the papyrus compiler BGS provides in the Starfield Game's Tool subdirectory.
- TOOL_PATH_ARCHIVER is the path to the archiver that BGS provides in the Starfield Game's Tool subdirectory.
- TOOL_PATH_XTEXCONV you can use the [DirectX Texconv Tool](https://github.com/microsoft/DirectXTex/releases)
- PAPYRUS_SCRIPTS_PATH the path to where papyrus scripts get stored in the Starfield Game Data folder
- PAPYRUS_SCRIPTS_SOURCE_PATH the path to the source subfolder in the papyrus scripts folder
- PAPYRUS_COMPILER_FLAGS currently the same as the PAPYRUS_SCRIPTS_SOURCE_PATH
- SPRIGGIT_VERSION if you use it this is the version of sprggit to use
- SPRIGGIT_PATH is the path to the spriggit CLI
- MODULE_DATABASE_PATH is the path to the Vortex/MO2 staging folder
- MODULE_SCRIPTS_PATH is the path to the scripts subfolder in the Vortex/MO2 staging folder
- MODULE_SCRIPTS_SOURCE_PATH is the path to the Source subfolder in MODULE_SCRIPTS_PATH
