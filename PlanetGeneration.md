# Planet Generation (PCM)

## New planet and system creation
- Creating a new system or planet requires a new game or at least a new NG+ universe

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
##### PCM_BlockCreationRequest ==PCMT:0005B625== and PCM_CellLoadRequest ==PCMT:0005B62B==
Block Creation Requests and Cell Load Requests essentially do the same thing but in different phases. Block creation is at world creation and cell load is when the player enters the cell usually via landing. 

For the most part block creation request create POI around the landing site, but there is also special rules for the area around outposts, settlements, and cities. These special outpost rules have higher priority so they win out in the end. 

##### PCM_QuestRequest ==PCMT:000F455A==
This generates custom surface blocks for quests to that the player can encounter and land at them. 

##### PCM_SpaceshipLandingRequest ==PCMT:00018BB1==
This handles clearing the area around and creating the landing area for your ship. 