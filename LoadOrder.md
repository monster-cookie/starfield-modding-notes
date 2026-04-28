# Load Order Finding

Starfield seems to have a few areas that require strict load order positioning. Also as a reminder BGS states and still does not recommend changing the load order or uninstalling mods mid game.

## Patching

You should also be confirming conflicts and patching them yourself in xEdit as this is the available best solution. If they are stable and the mod authors allow post those patches for other to use.

## Findings

The following items are high susceptible to breakage when their load order is changed and when changed they need a new game or if your lucky an immediate NG+ universe reset.

### Procedural Generation (PCM for example)

Procedural Generation rules when linked to mods cause planets to render incorrectly or even fail to load if rules with form IDs are changed to new IDs. Other then the Cell Reset rules PCM or as stated otherwise by the mod authors these changes need a new universe for changes to apply.

### Biomes

Related to PCM when the biome links are changed it flora/fauna weird mixes of old and new and even terrain problems can result. Again unless otherwise stated by the mod author, these changes always need a new universe.

### Leveled NPCs or NPCs (THis is still a little grey there is a problem here but its not locked down exactly)

Changes to NPCs and NPC Leveled lists using none vanilla records including copied vanilla records, can cause CTDs or mass conversions to level 1 humans (creatures do it to but can't remember their default record)

## ESM Limitations

There is currently (Pre CK) a limitation of approximately 150 ESMs (not mods) after which the engine has problems rendering textures, papyrus scripting breaks down, a general mess. So going over 150 ESMs is discouraged but if you experience issues pare back your ESM count and see if that helps

## Loose File Limitations

Loose files (Mainly textures) cause performance problems and scripting lag as the file counts increase. It is recommended to bundle loose textures into BA2 archives.

## Suggested Load Order Groups

These groupings are purely logical unless you are using MO2 or LOOT starts supporting Starfield again. But in any organizer or manually you can local the load order positions so that ESM's mod index remains fixed.

Groups with :lock: should not be moved under any circumstance

1. BGS Core :lock:
2. Core Fixes :lock:
3. Shared Libraries :lock:
4. Proc-Gen Overhauls (Biomes, Planets, Systems, and Stars) and Mods :lock:
5. AI Overhauls and Mods that change all NPCs :lock:
6. Large Overhauls
7. Early Loading Fixes
8. Early Loading Mods
9. Default
10. Late Loading Mods
11. Late Loading/Highly Specific Fixes

### Example Using Venworks

THIS IS AN EXAMPLE: Please follow the mod's and its author's specific instructions if they have them. 

ESMs and groups with :lock: should not be moved under any circumstance

01. BGS Core
  a. Starfield.esm :lock:
  b. Constellation.esm :lock:
  c. OldMars.esm :lock:
  d. BlueprintShips-Starfield.esm :lock:
02. Core Fixes
  a. StarfieldCommunityPatch.esm :lock:
03. Shared Libraries
  a. StarfieldCore.esm :lock:
  b. Venworks-Core.esm :lock:
04. Proc-Gen Overhauls (Biomes, Planets, Systems, and Stars) and Mods
  a. VenworksFactionOverhaul.esm :lock:
  b. VenworksEncountersOverhaul.esm :lock:
  c. GrindTerraformed.esm :lock:
05. AI Overhauls and Mods that change all NPCs
  a. CoraCanRead.esm :lock:
  b. CoraTheBookHunter.esm :lock:
  c. CoraCoeMultiversalBookHunter.esm :lock:
  d. GrindTerraIndustriesFaction.esm :lock:
06. Large Overhauls
07. Early Loading Fixes
  a. OutpostBuilderCategories.esm
08. Early Loading Mods
09. Default
  a. ScaleTheWorldTheSequel.esm
  b. ResizeTheWorld.esm
  c. GalacticPetShop.esm
  d. GalacticJunkRecycler.esm
  e. VenworksJunkRecycler.esm
  f. GalacticPawnShop.esm
10. Late Loading Mods
  a. VenworksDebugTools.esm
11. Late Loading/Highly Specific Fixes
  a. WalterFactionPatch.esm :lock:
