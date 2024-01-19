# Quests - Scenes

## Known Issues
- Scene phases that set parent quest quest stage don't work again have to use Dialog scripts to cheat.

## Scene Requirements
- Scene actions that trigger another scene require a 00 mod prefix which means we can't use them without dangerous injection.
    - Instead we have to use a dialog script linked to the scene action. They are supposed to be scene action scripts (like quest fragments) but I have not been able to get them to work at all.
    - I have gotten dialog response scripts to work

## Dialog Responses
- When using dialogue with conditions on the dialogue topic (DIAL) the responses with conditions need to be ordered first in the topic list. The topic list is processed in order and the first condition that is hit successfully stops and lower responses are ignored. Also any info responses with no conditions need to be at the bottom of the topic list.
