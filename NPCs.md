# NPCs

A lot of persistent NPC changes require NG+ reset, but you can sometimes spoof it with Disable/Enable and ResetInventory in the console. Companion resets are a lot more work. Also if the NPC is bound to a handler quests (think SQ_Crew, etc) you will have to reset the quest or use what ever reset path the quest script provides. Again see Companions for an example.

## Template Actors

| Template Actor  | Affects                                                                       |
| --------------- | ----------------------------------------------------------------------------- |
| Trait           | Appearance Data (From CK1: Race, Sex, VoiceType, & Death Items)               |
| Stats           | Stats (From CK1: Level, Attributes, Skills, and Class)                        |
| Factions        | Factions Field                                                                |
| Spell List      | Actor Effect Field                                                            |
| AI Data         | AIDT - AI Data                                                                | 
| AI Packages     | Packages field                                                                |
| Model/Animation | NPC Model and Animations                                                      |
| Base Data       | ??? (From CK1: Name, Long Name, Short Name, and Properties Field)             | 
| Inventory       | The Containers Items Field[^1]                                                |
| Script          | Attached scripts the VMAD field                                               |
| Def Pack List   | default package list                                                          |
| Attack Data     | ???, Combat Style maybe                                                       |
| Keyword         | The keywords field                                                            |
| Unknown13       | Reaction Radius RDSA Field                                                    |
| Unknown14       | ???                                                                           |

- Template actors fully override anything on the NPC records. For example Cora's initial dark hair and wrong hair cut bug were caused by the linked trait template actor's setting.
- Fields set in multiple template actors don't inherit only the specific template actor used for a field wins. 

[^1]: Currently inventory is not being pulled from template or base actors. 
