# Development Workflow

This document outlines the workflow I use when developing my Venworks Creations for Starfield. My goal is to provide a practical starting point for anyone who wants to create their own Starfield mods while also building safer development habits along the way. It covers how I use Git for backups, change tracking, and version history, so it is easier to understand why changes were made over time and to recover when tools like the Starfield Creation Kit, xEdit, or Git LFS decides to feed your work to the friendly neighborhood Terrormorph.

## Prerequisites

I don't use the BGS Papyrus plugin because it's pretty opinionated and requires working from specific directories that don't play well with Git-based development.

1) Need a public or private Git repo
2) Need SFCK
3) Need xEdit 4.1.5q. Only use the version from their Discord.
4) Need VS Code with [Papyrus Plugin](https://marketplace.visualstudio.com/items?itemName=joelday.papyrus-lang-vscode)
5) Need PowerShell
6) If you are not using MO2, you will need a file watcher to watch the Game Data directory and catch the random files the CK creates, such as terrain, geometries, etc. I recommend [FolderChangesView](https://www.nirsoft.net/utils/folder_changes_view.html).
7) Need Nifskope, available from the FO76utils fork: [FO76Utils Nifskope](https://github.com/fo76utils/nifskope)
8) Need ce2utils, available from the FO76utils GitHub repo: [FO76Utils CE2 Utilities](https://github.com/fo76utils/ce2utils)

## Standard Repository Layout

- `Spriggit/`: YAML source for the plugin, such as `Venworks-Core.esm`.
- `Papyrus/`: Papyrus source scripts.
- `Staging/`: Committed release-ready game files and generated outputs used by packaging. This is a folder junction to your Vortex/MO2 staging folder.
- `Tools/`: Local PowerShell workflows for setup, Papyrus compilation, Spriggit assembly, validation, and BA2 package generation.
- `Documentation/`: Project-specific documentation, including release packaging notes.
- `MarketingSites/`: Nexus and marketing assets.

## Repository Setup

This works best with MO2, but MO2 VFS hasn't been working well on later Windows 11 installs. I mean it works, but it causes noticeable lag and some tools like Nifskope and Spriggit don't play well with it.

### MO2

Coming soon. I need to use MO2 to sort out its compatibility issues with Creations Forge anyway.

### Vortex

Generally, these instructions only need to be done once.

1) Open SFCK and make a new ESP for your creation
2) Zip the ESP and move the zip to ~/Downloads
3) Delete the original ESP if it is still in the Game Data folder
4) Open Vortex and install the zip as a custom mod
5) Copy the files from one of my projects' `.vscode` folders
6) Copy all the files from the Tools folder of one of my projects
7) Edit sharedConfig.ps1, set $Global:ScriptingNamespaceModuleCompany, $Global:ScriptingNamespaceModuleName, $Global:ScriptingNamespaceSharedLibraryCompany, $Global:ScriptingNamespaceSharedLibraryName, and $Global:Databases
8) Create a .env file with no blank lines. See ENV Setup below in the References section.
9) Delete the `Staging` folder if it exists
10) Open VS Code and run Tasks > Run > Setup The Repo, this creates a folder junction with the MO2/Vortex staging folder

## Repository Helper Scripts

Most local workflows are driven through scripts in `Tools/`. They expect a configured `.env` and local Starfield/Creation Kit tooling. Most should have matching VS Code tasks preconfigured in the `.vscode` folder.

Common scripts:

- `Tools/setupRepo.ps1`: Prepare the local Vortex/MO2 folder junction.
- `Tools/checkRepo.ps1`: Validate the expected local staging setup. Unfortunately, Windows may randomly reset the junction; luckily, this is pretty rare.
- `Tools/compileScripts.ps1`: Compile Papyrus scripts and send the compiled scripts and source files to the staging folder. Run this any time you change Papyrus code.
- `Tools/SpriggitAssembleDatabaseFromYaml.ps1`: Assemble Spriggit YAML into the staged plugin file. This is dangerous because not all records are fully supported.
- `Tools/SpriggitDumpDatabaseToYaml.ps1`: Dump the ESM database into Spriggit YAML. Run this any time you change the ESM/ESP directly.
- `Tools/createPackages.ps1`: Create BA2 archives from staged content. Run this any time package/archive contents change.

## Normal Workflow

### Pre-Commit Checklist

Some repos commit generated artifacts so releases and packaging are reproducible from the repository. Before committing, make sure generated outputs match the source changes in the same commit.

- If `.psc` Papyrus source changed, compile Papyrus and commit the updated `.pex` files with the source changes.
- If Spriggit/YAML plugin source changed, assemble or update the plugin file before committing and include the updated staged plugin artifact.
- If staged package contents, loose files, scripts, assets, or archive inputs changed, regenerate the BA2 archives before committing.
- Check the repo-specific release or packaging docs for the exact staging paths, package contents, and generated artifacts that must be committed.

### Papyrus Scripts

1) Open VS Code
2) Make your edits
3) Run Tasks -> Run -> Compile Scripts
4) Run Tasks -> Run -> Package Archives
5) Open your Git IDE and commit the changes

### Game Database (ESP)

If you have Papyrus changes, make them before launching SFCK.

1) If not using MO2, remember to launch FolderChangesView and start monitoring with the file watcher
2) Open SFCK. If using MO2, you have to launch it from MO2.
3) Open the ESP
4) Make your changes
5) Use File -> Convert Archive (YOU MUST MATCH the ESM size type)
6) Uncheck the ESP from the load order
7) Launch Starfield and test
8) Open your Git IDE and commit the changes

## Releases

Releases are created from tags in `v<major>.<minor>.<patch>` format on `master`. The GitHub Actions release workflow packages only:

- `Staging/Venworks-Creation.esm`
- `Staging/*.ba2`

The workflow intentionally excludes `Staging/Venworks-Creation.esp`, loose scripts, source files, metadata, and local-only outputs.

Release notes come from the matching `## Version x.y.z` section in the repo's `CHANGELOG.md`. The same notes are converted to BBCode for the Nexus Mods description.

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
MODULE_DATABASE_PATH=C:\Users\username\AppData\Roaming\Vortex\starfield\mods\Venworks - Encounters Overhaul
MODULE_SCRIPTS_PATH=C:\Users\username\AppData\Roaming\Vortex\starfield\mods\Venworks - Encounters Overhaul\Scripts
MODULE_SCRIPTS_SOURCE_PATH=C:\Users\username\AppData\Roaming\Vortex\starfield\mods\Venworks - Encounters Overhaul\Scripts\Source
```

NOTE: .env can't process environment variables, go figure, so all paths must be fully qualified.

- STEAM_GAME_FOLDER is the path to the Starfield game folder. This is usually Steam, but the Game Pass/MS Store version can work too if you handle its more complicated Data path.
- STEAM_DATA_FOLDER is the Data subdirectory of the Starfield game directory. In Game Pass, this may be ~/Documents/My Games.
- TOOL_PATH_PAPYRUS_COMPILER is the path to the Papyrus compiler BGS provides in the Starfield game's Tools subdirectory.
- TOOL_PATH_ARCHIVER is the path to the archiver BGS provides in the Starfield game's Tools subdirectory.
- TOOL_PATH_XTEXCONV can point to the [DirectX Texconv Tool](https://github.com/microsoft/DirectXTex/releases)
- PAPYRUS_SCRIPTS_PATH is the path where Papyrus scripts get stored in the Starfield Game Data folder
- PAPYRUS_SCRIPTS_SOURCE_PATH is the path to the Source subfolder in the Papyrus scripts folder
- PAPYRUS_COMPILER_FLAGS is currently the same as PAPYRUS_SCRIPTS_SOURCE_PATH
- SPRIGGIT_VERSION, if you use it, is the version of Spriggit to use
- SPRIGGIT_PATH is the path to the Spriggit CLI
- MODULE_DATABASE_PATH is the path to the Vortex/MO2 staging folder
- MODULE_SCRIPTS_PATH is the path to the scripts subfolder in the Vortex/MO2 staging folder
- MODULE_SCRIPTS_SOURCE_PATH is the path to the Source subfolder in MODULE_SCRIPTS_PATH
