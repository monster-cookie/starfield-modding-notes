# Radiant Engine: Static

## Positional and Map Markers

### MapMarker (MapMarkerRefType) [REQUIRED]

Marker to the player spawn/fast travel point.

### REOverlayCenter (RECenterLocRef) [REQUIRED]

Marker to the center of the world space or cell. OEScript uses this as it's default spawn point so needs to be clear.

## Scene Markers

These are markers you can use for scene triggers, npc spawning, etc.

### REOverlaySceneA1 (RESceneA1LocRef) - REOverlaySceneA3 (RESceneA3LocRef)

### REOverlaySceneB1 (RESceneB1LocRef) - REOverlaySceneB3 (RESceneB3LocRef)

## Travel Markers

These are marker for NPCs to travel too, guard, or for use in patrol routes.

### REOverlayTravelA1 (RETravelA1LocRef) - REOverlayTravelA3 (RETravelA3LocRef)

### REOverlayTravelB1 (RETravelB1LocRef) - REOverlayTravelB3 (RETravelB3LocRef)

## NPC Markers

### REOverlayLeaderMarker (RELeaderMarkerLocRef)

This marker denotes where the group's leader would spawn. These aren't well used BGS seems to use the Scene and Travel markers instead.

NOTE: BGS does not use this method by far more they use REOverlayTrigger_AreaLeader (RETriggerAreaLeaderLocRef) route.

## POI Clutter Markers

These markers denote where packins or objects can be spawned and make sense in a POI. Their sizing tags denote how much free space around the marker there is.

Looks like BGS added the system in last minute which is why they probably only have support for large items.

### Ground Markers

These are objects and markers where is would make sense to spawn outdoor items for example a tent.

#### REOverlayMarkerLargeGround (REMarkerLargeGroundLocRef)

### Floor Markers

These would be where you would spawn in door items that don't need to sit on something for example a table.

#### REOverlayMarkerLargeFloor (REMarkerLargeFloorLocRef)
