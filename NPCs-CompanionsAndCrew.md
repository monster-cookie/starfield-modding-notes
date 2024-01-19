# NPCs - Companions and Crew

The biggest problem with custom companions is tracking all the quests, stages, scene locks, and the story gate global variables. Make sure you keep an excel spreadsheet or at least a document of some sort.

## Available Companion

This is controlled buy completion of MQ104b for the constellation companions. The NG+ script also handles this for variant universes where the companion might be dead or otherwise unavailable.

For custom companions, just make an init quest that calls in the OnQuestInit event: 
```
(SQ_Companions as SQ_CompanionsScript).SetRoleAvailable(StarbornCoraCoeREF, True)
(StarbornCoraCoeREF as CompanionActorScript).AllowStoryGatesAndRestartTimer()
```
This should handle both new characters and the NG+ purge.

## Known Issues
- Do not use Sam Coe as a basis for anything he is very bugged and implemented totally different then the other companions.
- Sarah Morgan is missing most of her conditions (SFCP has fixed this)