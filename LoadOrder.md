# Load Order Finding

Starfield seems to have a few areas that require strict load order positioning.

## Findings

The following items are high susceptible to breakage when their load order is changed and when changed they need a new game or if your lucky an immediate NG+ universe reset. 

### Procedural Generation (PCM for example)

Procedural Generation rules when linked to mods cause cause planets to render incorrectly or even fail to load if rules with form IDs are changed to new IDs. Other then the Cell Reset rules PCM needs a new universe for change to safely apply. 

### Biomes

Related to PCM when the biome links are changed it flora/fauna weird mixes of old and new and even terrain problems can result. Changes to biomes should have a new universe. 

### Leveled NPCs or NPCs (THis is still a little grey there is a problem here but its not locked down exactly)

Changes to NPCs and NPC Leveled lists can cause CTDs or mass conversions to level 1 humans (creatures do it to but can't remember their default record)

## ESM Limitations

There is currently (Pre CK) a limitation of approximately 150 ESMs (not mods) after which the engine has problems rendering textures, papyrus scripting breaks down, a general mess. So going over 150 ESMs is discouraged but if you experience issues pare back your ESM count and see if that helps

##  Loose File Limitations

Loose files (Mainly textures) cause performance problems and scripting lag as the file counts increase. It is recommended to bundle loose textures into BA2 archives. 

## Suggested Load Order Groups

Groups with :lock: should not be moved under any circumstance and groups with :unlock: generally can be moved

01. BGS Core :lock:
02. Core Fixes :lock:
03. Shared Libraries :lock:
04. Proc-Gen Overhauls (Biomes, Planets, Systems, and Stars) and Mods :lock:
05. AI Overhauls and Mods that change all NPCs :lock:
06. Large Overhauls
07. Early Loading Fixes
08. Early Loading Mods
09. Default
10. Late Loading Mods
11. Late Loading/Highly Specific Fixes

## Example Using Venworks and Royal Stuff

THIS IS AN EXAMPLE: Please follow the mod's and its author's specific instructions if they have them. 

ESMs and groups with :lock: should not be moved under any circumstance

01. BGS Core
  - Starfield.esm :lock:
  - Constellation.esm :lock:
  - OldMars.esm :lock:
  - BlueprintShips-Starfield.esm :lock:
02. Core Fixes
  - StarfieldCommunityPatch.esm :lock:
03. Shared Libraries
  - VenpiCore.esm :lock:
04. Proc-Gen Overhauls (Biomes, Planets, Systems, and Stars) and Mods
  - VenpiFactionOverhaul.esm :lock:
  - VenpiCaveOverhaul.esm :lock:
  - GrindTerraformed.esm :lock:
06. AI Overhauls and Mods that change all NPCs
  - CoraCanRead.esm :lock:
  - CoraTheBookHunter.esm :lock:
  - CoraCoeMultiversalBookHunter.esm :lock:
  - GrindTerraIndustriesFaction.esm :lock:
07. Large Overhauls
08. Early Loading Fixes
  - OutpostBuilderCategories.esm
08. Early Loading Mods
09. Default
  - ScaleTheWorldTheSequel.esm
  - ResizeTheWorld.esm
  - GalacticPetShop.esm
  - GalacticJunkRecycler.esm
  - GalacticPawnShop.esm
10. Late Loading Mods
11. Late Loading/Highly Specific Fixes
  - Patches for Venworks Faction Overhaul
