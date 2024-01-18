# Mod Research

This site is a collection of multiple peoples work and dedication and is meant to help new and aspiring mod authors develop new mods and content for Starfield.

## Tools

- xEdit 4.1.5b
    - This is the tool that even lets us mod right now. Thank you so much Elminster and the xEdit Team for your hard work and dedication. 
    - Currently cloning/overriding records with unknown reflection data cannot be copied
        - This is because we have no safe way to ensure there are not form IDs and function data that can cause in correct references and save corrupts/CTDs. 
        - There is an early version of xEdit that allows editing and transfer of REFL containing records. If you use it you MUST reverse the binary to strings to try and understand what the class/record is doing and more importantly if its is referencing other records via handles or form IDs. 
    - Only available on their discord which is locked down currently - [xEdit GitHub](https://github.com/TES5Edit/TES5Edit)
- nifskope
    - This allows for texture swaps and modifications of in game models and assets
    - Only available from a fork by FO76utils [FO76Utils Nifskope](https://github.com/fo76utils/nifskope)
- ce2utils 
    - A collection of tools for accessing Starfield data
    - Only available from GitHub repo by FO76utils [FO76Utils CE2 Utilities](https://github.com/fo76utils/ce2utils)

## Table of Contents
- [Creature System (CCT)](CreatureSystem.md)
- [CTD Causes](CTDCauses.md)
- [Message Records](MessageRecords.md)
- [NPCs](NPCs.md)
- [NPCs - Companions](NPCs-CompanionsAndCrew.md)
- [NPCs - Vendors](NPCs-Vendors.md)
- [Pack-ins](Pack-ins.md)
- [Perks](Perks.md)
- [Planet Generation (PCM)](PlanetGeneration.md)
- [Quests](Quests.md)
- [Quests - Scenes](Quests-Scenes.md)
- [Quests - Triggers](Quests-Triggers.md)
