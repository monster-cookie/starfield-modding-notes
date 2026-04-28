# Radiant Engine: Location References (LocRef)

There should also be a related XMarker or Activators to each of these Location Refs.

## Cell Markers

### RETriggerLocRef [REQUIRED]

This is the master marker that controls everything. In activator form, this is what fires the script event when the player gets in range.

### RETriggerExteriorLocRef [REQUIRED]

Marker for the exterior world space.

### RETriggerInteriorLocRef [REQUIRED]

Marker to/for the interior cell.

## Positional and Map Markers

### MapMarkerRefType [REQUIRED]

Marker to the player spawn/fast travel point.

### RECenterLocRef [REQUIRED]

Marker to the center of the world space or cell. OEScript uses this as it's default spawn point so needs to be clear.

### RETriggerPerimeterLocRef [REQUIRED]

## Scene Markers

These are markers you can use for scene triggers, npc spawning, etc.

### RESceneA1LocRef - RESceneA3LocRef

### RESceneB1LocRef - RESceneB3LocRef

## Travel Markers

These are marker for NPCs to travel too, guard, or for use in patrol routes.

### RETravelA1LocRef - RETravelA3LocRef

### RETravelB1LocRef - RETravelB3LocRef

## NPC Markers

### RETriggerAreaLeaderLocRef

This marker denotes where the group's leader would spawn.

### REScenePatrolStartLocRef and REScenePatrolEndLocRef

This denotes a patrol route NPCs could follow in the POI.

### RECorpseLocRef

This denotes where a corpse could be spawned in a POI and make sense.

### RECaptiveMarkerLocRef

This denotes where a captive can spawn in a POI and make sense.

### REWoundedMarkerLocRef

This denotes where a wounded NPC can spawn in a POI and make sense.

## Quests/Story Markers

### REContainerLocRef

A usable marker for where a chest could spawn.

## POI Clutter Markers

These markers denote where packins or objects can be spawned and make sense in a POI. Their sizing tags denote how much free space around the marker there is.

### Ground Markers

These are objects and markers where is would make sense to spawn outdoor items for example a tent.

#### REMarkerLargeGroundLocRef

### Floor Markers

These would be where you would spawn in door items that don't need to sit on something for example a table.

#### REMarkerLargeFloorLocRef