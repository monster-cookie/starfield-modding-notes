# NPC Voice Action Setup

In SF1Edit 4.5C unfold a Quest including dialogs, such as "CREW_EliteCrew_Astrid" here, and you'll have "Scene", "Dialog Branch" & "Dialog Topic" as possible tree childs, if you look into a "Dialog Topic", you'll have one or many "Info" child(s) ( Under SF1Edit, the "INFO" kind of the child only appears at right in the header while at left it's left blank ) 
This INFO is what contains both the text to-display and a link to the .wem voice-sound file the NPC will have to say.

It can contain multiple "Responses", each one including :

► TRDA , with 3 fields : An emotion field,  a link to the WEM, and an "unknown" Float number feature which I guess to be the intensity of the emotion (?) maybe from 0.0 to 10.0 ( Maybe more, 0 to 100 ?)

► Unknown ► TROT, with 2 fields : A link to the VoiceType used which you may have to create for a custom NPC, and here again a Float number I suspect to also be the intensity, but for the "Anim Face Archetype" tied to the VoiceType you chose / created...
Under TROT, in "NAM1 - Response Text" you'll have the Text to display.

About the wwise sound file (with the record of the text-to-speech), the .wem link can be a totally custom hexadecimal of 8 digits, except all the one I checked had "00" as to start with, thus I advice to keep that and to name each of your own sound file an unique 00xxxxxx.wem with each "x" being from 0 to F in hexa ( 0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F)

Then, if your mod name is "killthemall.esm", you have to create these (sub-)directories in the DATA folder of the game : Sound/Voice/killthemall.esm/TheVoiceTypeName/

"TheVoiceTypeName" must be the name after the "VoiceType" object you chose or created in SF1Edit and which is tied to your INFO dialog as exmplained upper (and also to your NPC who has a field for VoiceType).

Inside that directyory, you can thus copy all your .wem files ( I made mine more or less in following this tutorial if it can help ) and name each file as explained above : On my side I found it useful to keep the last 8 hexa digits from an INFO record as the same one for the first .wem it may use because it is easier to link INFO records to .wem files that way, however according to your own mod records HEXA base it might be more or less tricky ; In the end you might do it any way you want, the only thing being you must obviously name the .wem after the one you edited in the wem field in SF1Edit.

[See https://www.nexusmods.com/starfield/mods/8209/?tab=posts&jump_to_comment=136055424](https://www.nexusmods.com/starfield/mods/8209/?tab=posts&jump_to_comment=136055424)
