# Radiant Engine: POI Setup

The radiant engine uses Story Manager Script Event node to process the dynamic POI setup and spawning of items and NPCs. The initial entry point is the RETriggerOverlay activator which applies a RETriggerLocRef location reference to the POI interior/world space cell.

## Required Instructions

1. The cell MUST have a RETriggerOverlay activator marker added to it and it's attached RETriggerScript configured. This activator should be towards the edge in a safe place for the player to spawn. Generally the MapMarker goes here too.
2. You need to place the fast travel/map marker MapMarker static. Ideally this should be at the same safe place as the trigger marker.
3. In the center of the cell in a safe place for NPCs to travel too, place the REOverlayCenter (RECenterLocRef) static marker.
4. You should place a container maker in depending on the zone type:
  a. Human use REOverlayContainerHuman container
  b. Animal use REOverlayContainerNatureCreature
  c. For all others use REOverlayContainerNatureBarren
5. You need to place at least the 3 A class travel and scene markers. If the POI is large enough you should place the B class markers too.
6. You need to place the REOverlayTrigger_AreaLeader activator

## Optional Instructions

- Optionally and if the POI is large enough you should place the REOverlayCaptiveMarker captive furniture markers.
- Optionally and if the POI is large enough you should place the REOverlayWoundedMarker wounded NPC furniture marker.
