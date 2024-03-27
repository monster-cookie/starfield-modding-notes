# Starfield Modding Issues

## Subsections
- [CTD Causes](./CTDCauses.md)

## Mod Indexes
Each ESP/ESM in Starfield requires a mod index in order to resolve and find its resources. This is an unsigned short integer so the absolute maximum number of them is 255, really 254. Then you lose 1 to ESL support, 1 for the main game ESM, and 1 to the main game EXE so we lose another 3 dropping us to 251 available indexes. BGS reserve another 8 for DLC dropping use down to around 242 for use in mods. 

Now there appears to be issues that start around 150 ESM and becoming impossible to use by 180 (crash to desktops on load). So for now you should keep to the absolute minimum mods you need vs want to have. 

## BA Archives

Also recently there is finding with measured proof that loose files cause significant performance issues and crashes. So it recommended if an author hasn't to merge the loose files for a mod into a BA2 or BA2v3(for pure textures only) archive. Non texture files should go in a archive named "<modnam> - Main.ba2" and texture can go in main or a file named "<modnam> - Textures.ba2" using the new version 3 BA2 format.

## Missing Textures and other collateral damage issues

Missing textures mostly, but as we found out last night overriding to reverse settings can also cause this, the papyrus system library (Game, Utility, MAth) native functions will start returning None. The most obvious side effect is Game.GetForm() and Game.GetFormByFile() which cause wide spread damage as expected forms are no longer there. 

Another common side effect is in game cities, POI, NPCs, will go invisible like their markers will still be there but the object no longer renders. 
