# Radiant Engine: Trigger Conditions

The radiant overlays and quests are controlled by the Story Manager Script Event

- Required Keyword to trigger and link a POI
  - SM OE_MainBranch Node requires REEncounterTypeOverlay be set
  - Child branches of this require NonBaseGameLocation be set
    - Unfortunately this tier is stacked not random
    - I suspect I will have to add my own branch here probably higher then OE_SpecialBranch in order to get them to trigger with any regularity
  - Actual quest triggers
    - BiomeSupportsCreature (function) takes an actor type
    - IsTrueForConditionForm (function) use PCM_HumanPresenceCondition or PCM_CND_BlockCreation_HabitabilityCheck to see if human presence
    - LocTypeOE_Theme*
