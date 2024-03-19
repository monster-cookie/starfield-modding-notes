# Naming Conventions

THese are the naming conventions I use for my projects that are based on BGS convetions. 

## Quests

- [PREFIX]_[Name]_[Type]_[Subtype]

### Prefixes

- COM = Companion Stuff
- MQ = Main Quests
- LC = Side Quests
- SQ = Scripted Quests (Quest managers for scripts mostly)
- RQ/MB = Random Quests
- SE = Space Encounter Quest
- OE = Open World Encounter (Planet)
- UC/FC/RI/MS/FF = Faction

### Examples

- COM_Companion_StarbornCoraCoe
- COM_Companion_StarbornCoraCoe_SpeechChallenges

## Scenes

- [QUEST]_[Type]_[Subtype]
### Examples

- COM_StarbornCoraCoe_System_AngerScene
- COM_StarbornCoraCoe_TopLevel_Personal

## Dialog Topic

### Standalone

- [QUEST/SCENE]_[P##]_[D##]
	- P## = Scene Phase
	- D## = Dialog Number

### Scene Linked

- [QUEST/SCENE]_[P##]_[D##/PD##]_[B##]_[PS/NR]
	- P## = Scene Phase
	- D## = Dialog Number

- [PD##]_[B##]_[PS##/NR##] = Dialog Branch
	- PD## = Dialog Tree Number
	- B## = Tree Branch Number
	- PS = Player Statement (can only be 1 per branch)
	- NR = NPC Response (can only be 1 per branch)

## Response Groups

- [DIALOG]_G##_[TAG]
	- G## = Group Number
	- TAG = See "Response Group Tags" section

### Response Group Tags

- AFF = Affection
- NEU = Neutral
- AGR = Angry
- POS = Positive
- NEG = Negative
- LKD = Quest/Story Locked
- ROM = Romance
- FND = Friendly
- LOC = Location Based

## Responses

- [DIALOG/Response Group]_R##
