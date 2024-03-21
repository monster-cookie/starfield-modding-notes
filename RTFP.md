# Real Time Form Patcher (RTFP)

[Real Time Form Patcher (RTFP)](https://www.nexusmods.com/starfield/mods/8324) is a SFSE mod that will allow dynamic injection and modification of engine records during the game load phase. 

## Support Matrix
| Starfield Record                             | Min Version | Keywords | Conditions | Full Name |
|----------------------------------------------|-------------|----------|------------|-----------|
| [Global Variable](./RTFP.md#global-variable) | 1.00        | N/A      | N/A        | N/A       |
| [Game Settings](./RTFP.md#game-settings)     | 1.00        | N/A      | N/A        | N/A       |
| [Conditions](./RTFP.md#conditions)           | 1.18        | N/A      | N/A        | N/A       |
| [MiscObject](./RTFP.md#misc)                 | 1.00        | Yes      | N/A        | Yes       |
| Leveled Base Form                            | 1.00        | N/A      | Yes        | N/A       |
| Leveled Item                                 | 1.00        | N/A      | Yes        | N/A       |
| Leveled NPC                                  | 1.00        | N/A      | Yes        | N/A       |

## Sections

* [Selector](./RTFP.md#selectors)
* [Configuration](./RTFP.md#configuration)
* [Global Features](./RTFP.md#global-features)
* [Filters](https://www.nexusmods.com/starfield/articles/463)
* [Custom Filters](https://www.nexusmods.com/starfield/articles/464)
* [Conditions](./RTFP.md#conditions)
* [Keywords](./RTFP.md#keywords)
* [Full Name](./RTFP.md#full-name)
* [Game Settings](./RTFP.md#game-settings)
* [Global Variable](./RTFP.md#global-variable)
* [MiscObject](./RTFP.md#misc-item-misc)
* [Planet Content Manager Branch Node (PCBN)](./RTFP.md#planet-content-manager-branch-node-pcbn)

## Configuration

### INI File

The settings file for RTFP lives in \<gamedir\>\\Data\\SFSE\\Plugins and must be named RealTimeFormPatcher.ini 

Settings in it currently (1=Enable/0=Disable): 
* bShowLoadedMessage - Show a console message when RTFP has fully loaded all files
* bShowWarningsAsMessageBox - Use a warning box instead of notification for warning messages
* bDebugMode - Turn on debug mode and process the \[Debug\] section

### RTFP Configuration Files

The configuration files for RTFP live in \<gamedir\>\\Data\\SFSE\\Plugins\\RealTimeFormPatcher and must be globally uniquely named.


## Global Features

### Minimum Version

If you set the first line of the file minver=\<version\> you can specify the minimum version of RTFP needed to process the file. If the user tries to load the RTFP file on an unsupported version of RTFP at run time they will get a Message Box popup. 

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

### Only Run If Plugin Loaded

You can add check to the first line so that the file only processed if the required plugin is loaded. You can optionally set it to notify the user the required plugin is missing.

#### Example 
```
minver=117|onlyifpluginloaded=MyTestPlugin.esm()
minver=117|onlyifpluginloaded=MyTestPlugin.esm(notify)
```

### Debug Mode 

Debug diagnostics were added in version 1.09 and lets you see in the log file the record processing and a dump of the final objects created. Debug mode causes a very noticeable processing lag so you should definitely disable it when its not needed and before releasing the RTFP file to anyone. This also requires bDebugMode set to 1 in the RealTimeFormPatcher.ini. 

Currently supported forms that can be dumped in debug 
* Activator
* AVM Data
* Condition Form
* Container
* Form Lists
* Leveled Lists
* Message
* NPC
* OMOD
* Weapon

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

### Selectors

You can either use the Editor ID or the ESM filename with a FormID to reference objects. If chaining multiple selectors like filters you need to prefix the line with a plus (+).

#### Examples 
```
[Global]
COM_EventReaction_Dislikes|val(0)
OE_ChanceUniqueGlobal|val(40)
Starfield.esm~0030BFFE|val(60)
+Starfield.esm~0030BFFE,Starfield.esm~0030BFFE|val(60)
```

#### Editor IDs
You can use editor IDs in most places that a form ID can be used but you need the [Power Of Three SFSE](https://www.nexusmods.com/starfield/mods/3621) mod. Without it you can only use them in specific places where the engine doesn't discard editor IDs as comments. 

Known Safe Places without the additional mod
* Game Settings
* Globals

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
  * Not equal (!=)
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

## Full Name

For record types that support naming you can set with the name() function

## Example
```
[Misc]
# Change vacuum tape to duct tape 
Starfield.esm~002AC95F|name("Duct Tape")
```

## Game Settings 

### Template
```
<GameSetting>:<Value>
```
* Game Setting must match the name of the Game Setting from Starfield.exe, Starfield.esm, or the Engine
* Value can be a string (wrapped in quotes), Integer, or a Float.

### Example
```
[GameSettings]
fHandScannerBaseRange|100.00
iAINumberActorsComplexScene,iNumberActorsInCombatPlayer|60
sAffinityEventHates|"disagrees."
```

## Global Variable

### Template
```
<Selector>:<Function>
```
* Selector - The selector to find the item to edit
* Valid Functions
  * val(\<value\>) - Set the referenced global to value where value is a Float or Integer

### Example
```
[Global]
COM_EventReaction_Dislikes|val(0)
OE_ChanceUniqueGlobal|val(40)
Starfield.esm~0030BFFE|val(60)
```

## Misc Item (Misc)

### Template
```
<Selector>:<Function>|...|<FunctionN>
```
* Selector - The selector to find the item to edit
* Valid Functions
  * model(\<path\>) - Set the path to the model to path where path is a quoted string
  * val(\<value\>) - Set the value of the item to value where value is a float

### Example
```
[Misc]
# Tool_DuctTape01 "Vacuum Tape" [MISC:002AC95F]: Small Size - Tier A (Adhesive) - Tier B (Fiber) - Tier C (Alkanes) - Tier D (None)
Starfield.esm~002AC95F|kwd_add(VenworksJunkRecycler.esm~0000080E)|kwd_add(VenworksJunkRecycler.esm~00000803)|kwd_add(VenworksJunkRecycler.esm~00000811)|kwd_add(VenworksJunkRecycler.esm~00000816)
```

## Planet Content Manager Branch Node (PCBN)

Block Creation rules need to exist at universe creation time in my experiments RTFP hooks in too late for them, but Cell Reset rules are processed at landing/fast travel so these can safely be modified with RTFP. Removing nodes requires a new game or a new NG+ universe and will cause a CTD if loading a planet with a removed node. 

### Template
```
<Selector>:<Function>|...|<FunctionN>
```
* Selector - the selector to find the item to edit
* Valid Functions
  * node_add(\<Selector\>) - Add a node using the specified selector. 
  * node_rmv(\<Selector\>) - remove a node using the specified selector. 
  * node_rpl(???) - Replace a node with another node. 
  * mode_clr() - Clears all nodes

### Example
```
[PCBN]
Starfield.esm~2C4EA|node_add(Starfield.esm~5FF75)
```
