This site is a collection of multiple peoples work and dedication and is meant to help new and aspiring mod authors develop new mods and content for Starfield.

## Tools
- VS Code
  - Open Source editor from Microsoft
  - [Get from Microsoft](https://code.visualstudio.com/download)
- xEdit 4.1.5d 
  - This is the tool that even lets us mod right now. Thank you so much Elminster and the xEdit Team for your hard work and dedication. 
  - Currently cloning/overriding records with unknown reflection data cannot be copied
    - This is because we have no safe way to ensure there are not form IDs and function data that can cause in correct references and save corrupts/CTDs. 
    - There is an early version of xEdit that allows editing and transfer of REFL containing records. If you use it you MUST reverse the binary to strings to try and understand what the class/record is doing and more importantly if its is referencing other records via handles or form IDs. As of March 2024 this version not longer creates valid ESMs the current game and xedit's can read. 
  - You must be on 4.1.5b or later earlier versions missed some header record that break things.
  - Only use the version from their discord
    - [xEdit GitHub](https://github.com/TES5Edit/TES5Edit)
    - [xEdit Discord](https://discord.com/channels/471930020454072348/518048160526893057)
- nifskope
  - This allows for texture swaps and modifications of in game models and assets
  - Only available from a fork by FO76utils [FO76Utils Nifskope](https://github.com/fo76utils/nifskope)
- ce2utils 
  - A collection of tools for accessing Starfield data
  - Only available from GitHub repo by FO76utils [FO76Utils CE2 Utilities](https://github.com/fo76utils/ce2utils)

# Markdown
- GitHub's [Basic formatting and syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- GitHub's [Advanced Formatting, Tables](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-tables)
- Github's [Advanced Formatting, Task Lists](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/about-task-lists)

## Table of Contents
- [Starfield Modding Issues](./KnownModdingIssues.md)
- [Starfield Load Order Issues](./LoadOrder.md)
- [Starfield Naming Conventions](./NamingConventions.md)
- [Cell Reset](./CellReset.md)
- [Creature System (CCT)](./CreatureSystem.md)
- [CTD Causes](./CTDCauses.md)
- [Factions](./Factions.md)
- [Ingestibles](./Ingestibles.md)
- [Leveled Lists](./LeveledLists.md)
- [Map Markers](./MapMarkers.md)
- [Message Records](./MessageRecords.md)
- [Magic Effects](./MagicEffect.md)
- [NPCs](./NPCs.md)
- [Real Time Form Patcher \(RTFP\)](./rtfp.md)
- [Pack-ins](./Pack-ins.md)
- [Perks](./Perks.md)
- [Planet Generation (PCM)](./PlanetGeneration.md)
- [Spells](./Spells.md)
- [Quests](./Quests.md)
- [World Space Cells](./WorldSpaceCells.md)
