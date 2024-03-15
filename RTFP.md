# Real Time Form Patcher (RTFP)

Real Time Form Patcher (RTFP) is a SFSE mod that will allow dynamic injection and modification of engine records during the game load phase. 

## Support Matrix
| Starfield Record  | Min Version | Keywords | Conditions |
| Global Variables  | 1.0         | N/A      | N/A        |
| Game Settings     | 1.0         | N/A      | N/A        |
| Conditionals      | 1.18        | N/A      | N/A        |
| MiscObject        |             | Yes      | N/A        |
| Leveled Base Form |             | N/A      | Yes        |
| Leveled Item      |             | N/A      | Yes        |
| Leveled NPC       |             | N/A      | Yes        |

### Global Features

### Minimum Version

If you set the first line of the file minver=<version> you can specify the minimum version of RTFP needed to process the file. If the user tries to load the RTFP file on an unsupported version of RTFP at run time they will get a Message Box popup. 

Versions are entered as a non-decimal value for example 1.00 is entered at 100 and 1.12 as 112. 

#### Example 
```
minver=112
```

### RTFP File Load Order/Priority

You can control the load order of your file versus other files but specifying a priority that is lower then other files. The default priority is 0 and they are processed in alphabetical order for all files at the same priority. Valid range for priorities is -128 to 128. It is strongly recommended to not use this feature unless you have a strong need. 

#### Example 
```
minver=112|priority=-10
```

### Debug Mode 

Debug diagnostics were added in version 1.09 and lets you see in the log file the record processing and a dump of the final objects created. Debug mode causes a very noticeable processing lag so you should definitely disable it when its not needed and before releasing the RTFP file to anyone. This also requires bDebugMode set to 1 in the RealTimeFormPatcher.ini. 

Currently supported forms that can be dumped in debug 
* Form Lists
* Leveled Lists
* AVM Data

#### Example 
```
[Debug]
Starfield.esm~6F48|
SimpleGroup_Cheeks2|
SimpleGroup_CHARGEN_Cheeks2|
SimpleGroup_Cheeks1|
SimpleGroup_CHARGEN_Cheeks1|
SimpleGroup_Hair_Choppy|
```

### Comments

Any line that starts with a pound sign (#) is treated as a comment and ignored by the parser. 


## Conditions

Condition support was added in 1.17 Beta 3 and the new section needs to be before any entity that will consume the defined condition entries. 

### Caveats 
* Currently RunOn references are not supported
* String comparisons are not working currently

### Usage

Condition entries follow this template:
```
ConditionName:RunOn:ComparisonOperator:Value:param1:param2:flags
```
* ConditionName must be globally unique across all RTFP files
* Valid values for RunOn
  * Target
  * CombatTarget
  * LinkedReference
  * QuestAlias
  * PackageData
  * EventData
  * CommandTarget
  * EventCameraRef
  * MyKiller
  * Player Ship
* Valid Values for ComparisonOperator
  * Equal (=)
  * Not equal (<> or !=)
  * Greater Than (>)
  * Greater Than or Equal To (>=)
  * Less Than (<)
  * Less Than or Equal To (<=)
* Values can currently only be a integer or float
* Parameters are dictated by the plugin and are an integer or float. 
* Flags are optional 
  * or - Use or logic instead of and for the next condition. Or conditions must be at the end of the condition list. 
  * use_pdata - Use event data
  * use_alias - Use a quest alias
  * swap_subtar - Swap target and subject values in the query

### Example 

```
[Condition]
ConditionOne|Subject:GetRandomPercent:<=:1:~:~:or:use_alias
ConditionTwo|Subject:GetRandomPercent:=:2:~:~
ConditionThree|Subject:GetRandomPercent:>=:Starfield.esm~B71:~:~:swap_subtar
ConditionFour|Subject:GetWantBlocking:=:0:~:~:
ConditionFive|Subject:IsTrueForConditionForm:=:45:Starfield.esm~17B850:~|Subject:GetWantBlocking:=:0:~:~:

[ConditionForm]
Starfield.esm~28FB6|cnd_add(ConditionFour)
Starfield.esm~28FB6|cnd_add(ConditionSeven)

[LVLLBaseForm]
Starfield.esm~7317|cnd_add_to_entr(Starfield.esm~1E052A:1:1:0_ConditionTwo)
```

## Keywords 

Keywords can be added to any record that supports keywords. 

### Functions

* kwd_add - Add a keyword to the record
* kwd_rmv - Remove a keyword from a record
* kwd_rpl - Replace a keyword on a record with a new keyword
* kwd_clr - Clear all keywords from the record

### Example
```
[Misc]
# Tool_DuctTape01 "Vacuum Tape" [MISC:002AC95F]: Small Size - Tier A (Adhesive) - Tier B (Fiber) - Tier C (Alkanes) - Tier D (None)
Starfield.esm~002AC95F|kwd_add(VenworksJunkRecycler.esm~0000080E)|kwd_add(VenworksJunkRecycler.esm~00000803)|kwd_add(VenworksJunkRecycler.esm~00000811)|kwd_add(VenworksJunkRecycler.esm~00000816)
```
