# Planet Generation (PCM)

## New planet and system creation
- Creating a new system or planet requires a new game or at least a new NG+ universe
  - PCM Cell Load Request rules do not require a new game or NG+ universe you just need to fly to a new area of the current planet or a new planet. 

### Houdini
- So Houdini is the procedural terrain generation using Houdini software from [https://www.sidefx.com/products/houdini/](https://www.sidefx.com/products/houdini/ "https://www.sidefx.com/products/houdini/"). 
- The HoudiniData records on various objects Boimes, Planets, Stars configure the generation system and link in the cells. 
- Though mostly this package works with and requires Unreal 5+ BGS must have linked the systems somehow. 
    - Might lend some credence to the Unreal 5 rumors for post CE2/CK2 world.

## Starmap
- System level is UI capped at 99 but the engine allows up to the max of 999 
- Range of the starmap is -25, -25, -8 to 5, 5, 8 
    - If you create a system out of bounds sometimes the system level will show up as 0  or the system will not display on the map

## PCM Creation System

### Manager Tree
The manager tree function as the master control rules. The whole process starts here. 

#### Key Records
There is a necessary 1 to 1 relationship between Branch Nodes and content nodes and even better the system will allow you with no error to add the same content record to multiple brach creation rules. 

##### PCM_BlockCreationRequest ==PCMT:0005B625== and PCM_CellLoadRequest ==PCMT:0005B62B==
Block Creation Requests and Cell Load Requests essentially do the same thing but in different phases. Block creation is at world creation and cell load is when the player enters the cell usually via landing. 

###### PCM_BlockCreation_ClusterNearLocation_Caves
This is creates cave POI around the ship landing zones and new POI around your current POI up to the POI block limits.

###### PCM_BlockCreation_NearLocation_Outposts_Caves
This is creates cave POI around an outpost, settlement, and city.

###### PCM_BlockCreation_OEWorlds_Caves
This creates random cave POI around the block at creation.

###### PCM_BlockCreation_OEWorlds_Natural
This creates random natural and trait POI around the block at creation this is most of the POI you see when you land and explore. 

###### PCM_BlockCreation_OEWorlds_HumanHabitation
This create random ruins and human POI around the block at creation. 

##### PCM_QuestRequest ==PCMT:000F455A==
This generates custom surface blocks for quests to that the player can encounter and land at them. 

##### PCM_SpaceshipLandingRequest ==PCMT:00018BB1==
This handles clearing the area around and creating the landing area for your ship. 

## PCM Rule processing
Rules are process in order (Bottom First) starting with PCM_BlockCreationRequest [PCMT:0005B625] and PCM_CellLoadRequest [PCMT:0005B62B] the first child of a nods that's conditions evaluate true win for the sub block (PCM Block requests) or a cell for (PCM cell request). PCM cell requests can add more then 1 result in a cell and usually have distance checks to them too. 

When a rule branch is traversed a a leaf must be return or bad things happen. The engine seems to just grabs a random leaf if one isn't returned. This is why the branch rules and leafs generally have near identical conditions. This prevents the branch from being traversed when there is a possibility of no leaf being available.

### New Game/NG+ Universe
- Changes to PCM Block Creation rules require a new universe (either new game or new game plus) in order to be applied.
- Changes to PCM Cell Request rules only need travel to a new location on the current planet or to a new planet. 

## PCM Pack-In Lair System
These require a specific ordering of a chain of packing to function and the base uses Unkown11 for bulldozing so cannot be used with any active items like containers, triggers, lights, etc. 

Proper ordering base with bulldoze properties -> Active layer (Lights, Furniture, Markers, Spawners) -> PCM Target (This is added to the PCM Cell Request Rule)
