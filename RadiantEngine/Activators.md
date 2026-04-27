# Radiant Engine: Activators (LocRef)

There should also be a related Location Ref to each of these Activators.

## Cell Markers

### RETriggerOverlay (RETriggerLocRef) [REQUIRED]

This is the master marker that controls everything. In activator form, this is what fires the script event when the player gets in range.

This must have the RETriggerScript bound and configured to it. This script is what fires the REEncounterTypeOverlay Story Manager Script Event.

### REOverlayTriggerExterior (RETriggerExteriorLocRef) [REQUIRED]

Marker for the exterior world space.

### REOverlayTriggerInterior (RETriggerInteriorLocRef) [REQUIRED]

Marker to/for the interior cell.

## Positional and Map Markers

### REOverlayTriggerPerimeter (RETriggerPerimeterLocRef)

## NPC Markers

### REOverlayTrigger_AreaLeader (RETriggerAreaLeaderLocRef)

This marker denotes where the group's leader would spawn. These aren't well used BGS seems to use the Scene and Travel markers instead.

NOTE: This is by far the way BGS uses this marker.
