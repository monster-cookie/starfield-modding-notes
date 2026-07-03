# Starfield Modding/Creations/SFCK Notes

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

## Markdown

- GitHub's [Basic formatting and syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- GitHub's [Advanced Formatting, Tables](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-tables)
- Github's [Advanced Formatting, Task Lists](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/about-task-lists)

## Table of Contents

### Troubleshooting

- [Cell Reset](./Troubleshooting/CellReset.md)
- [CTD Causes](./Troubleshooting/CTDCauses.md)
- [Starfield Modding Issues](./Troubleshooting/KnownModdingIssues.md)
- [Starfield Load Order Issues](./Troubleshooting/LoadOrder.md)

### Modding

- [My SFCK Workflow](./Modding/Workflow.md)
- [Starfield Naming Conventions](./Modding/NamingConventions.md)

### Systems

- [Creature System (CCT)](./Systems/CreatureSystem.md)
- [Planet Generation](./Systems/PlanetGeneration.md)

### Major Record Types

- [Factions](./MajorRecordTypes/Factions.md)
- [Ingestibles](./MajorRecordTypes/Ingestibles.md)
- [Leveled Lists](./MajorRecordTypes/LeveledLists.md)
- [Message Records](./MajorRecordTypes/MessageRecords.md)
- [Magic Effects](./MajorRecordTypes/MagicEffect.md)
- [Pack-ins](./MajorRecordTypes/Pack-ins.md)
- [Perks](./MajorRecordTypes/Perks.md)
- [Spells](./MajorRecordTypes/Spells.md)
- [World Space Cells](./MajorRecordTypes/WorldSpaceCells.md)

#### NPCs

- [NPCs](./NPCs/NPCs.md)
- [Companions and Crew](./NPCs/NPCs-CompanionsAndCrew.md)
- [Vendors](./NPCs/NPCs-Vendors.md)
- [NPC Voice Setup](./NPCs/NPCs-VoiceSetup.md)
- [Leveled NPCs](./NPCs/LeveledList-NPC.md)

#### Quests

- [Quests](./Quests/Quests.md)
- [Scenes](./Quests/Quests-Scenes.md)
- [Triggers](./Quests/Quests-Triggers.md)

#### Other

- [Map Markers](./MapMarkers.md)
