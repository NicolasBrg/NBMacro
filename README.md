# NBMacro Pure Forge 1.12.2 - Version 1.8.2021_Release
A very easy to use mod to create macros, command sets and automatic behaviors on your servers. 

# Demo Video
*Click to play*<br>
[![Demo video](http://i3.ytimg.com/vi/-DnizHyhOv8/maxresdefault.jpg)](https://www.youtube.com/watch?v=-DnizHyhOv8)

## Permission
To use the macros you must have the permission "**nbmacro.admin**". Each macro then has a permission that you can configure directly. Please avoid to give access to macro commands to your player, because you can start a macro for every player on the server if you have the macro permission. 

## Available commands
### /nbmacro \<MacroName\> {TargetedPlayer} {ARGS_2} {ARGS_3} ... {ARGS_N}
You can define as many arguments as you want, these have aliases available in the execution of the macros, in the example:<br>
"**/nbmacro AmazingWelcome NicolasBrg Hey!**"<br>
**{ARGS_0}**, **{ARGS_1}** and **{ARGS_2}** will become respectively "**AmazingWelcome**", "**NicolasBrg**" and "**Hey!**"
  
This command starts the execution of the macro chosen for the targeted player, if player is left empty, the player executing the command will have the execution of the macro.
  
### /nbmacro_network {Server Name}
Load, update, or get information about your licence. (Only in the first setup)

### /nbmacro_admin \<Info | List | Stop\>
#### Info
Say how many macro are running at the time you sent the command
  
#### List
Display the list of all macro currently running with all available informations. (Name, permission, State, Count, Progress, ...)
  
#### Stop
Force the end of all macro (all steps will be processed until end), then they will be deleted.
  
## How that work?  
A macro requires to have the permission filled in configuration, with a list of commands that will be executed in order. Each instruction is numbered from 0. A safety counter is proposed to avoid an infinite loop, so each macro can execute up to a total of 1000 instructions. Each instruction has many aliases, here is the list:
  - **{PLAYER}**    :     Player name
  - **{X}**         :     Player x position
  - **{Y}**         :     Player y position
  - **{Z}**         :     Player z position
  - **{X_LOOK}**    :     Player look x position
  - **{Y_LOOK}**    :     Player look y position
  - **{Z_LOOK}**    :     Player look z position
  - **{WORLD}**     :     Player world name
  - **{ARGS_0}, {ARGS_1}, {ARGS_2}, ..., {ARGS_N}**   :   All arguments from the original commands will be replaced here
  
### Available commands
#### PM \<PLAYER\> <Message with space and color alias "&"> \_Hover text showed\_ #Command on click#
Send a private message to the targeted player.<br>

**For example:**<br>
  ``PM {PLAYER} &2Welcome &6{PLAYER}&2 do you a welcome message? _&2Click_ #Welcooooome !#`` Send the message "Welcome {PLAYER} do you a welcome message?" with color to the targeted player, with a green text hover "Click", and the execution of the command between "#" symbols. If it's a command, that will be executed, if it's a text, the message will be sent on click, here, if the player click, the message "Welcooooome !" will be sent on global chat.
  
#### BROAD \<Message with space and color alias "&"\> \_Hover text showed\_ #Command on click#
Send a broadcast message to every connected player.

**For example:**<br>
  ``BROAD &2Something will happen``: Send the message to everyone "Something will happen" colored in green (**&2** alias).<br>
  
#### LOG \<Message with space\>
Send a message in console.

**For example:**<br>
  ``LOG Something will happen``: Send the log message "Something will happen" to the server.<br>
  
#### CMD \<COMMAND\>
Execute the command. <br>
  **@r** will be replaced by a random player name.<br>
  **@a** will be replaced by the name of all online player. The command will be executed for each player.<br>
If you want the command be execute by the server, start it by "!", if you want the command will be executed by player, use "/". <br>
  
**For example:**<br>
  ``CMD !say Hello``: Will execute the command "say Hello" from the server<br>
  ``CMD !effect @a minecraft:regeneration 12 12``: Will execute the effect command from the server for each player<br>
  ``CMD /spawn``: Will simulate the player executing "/spawn" commands
    
#### OPEN \<Macro_Name\> \<@a | @r | PlayerName\> {ARGS_3} ... {ARGS_N}
As **CMD** command "@a" and "@r" are available here. Open a macro for the targeted player with as many args you want.
  
**For example:**<br>
  ``OPEN RankGive {PLAYER} @r Epic``: Execute the macro "**RankGive**" to a random player with "**Epic**" as argument for "**{ARGS_2}**"<br>
  
#### WAIT \<Seconds\>
Wait \<SECONDS\> seconds before continuing the macro execution.

**For example:**<br>
  ``WAIT 3``: Wait 3 seconds before continue the macro execution.<br>
  
#### GOTO \<Instruction ID\> {COUNT_LIMIT} 
Jump to the instruction ID you want while the count isn't reach.
  
For our example we consider the example defined in configuration as follows:
```json
  "Thunder": {
    "Permission": "nbmacro.amazing_welcome",
    "NeedToBeSaved": false,
    "Macro": [
      "PM {PLAYER} &eThunder is with you",
      "CMD !effect {PLAYER} minecraft:resistance 30 2",
      "CMD !effect {PLAYER} minecraft:levitation 1 5",
      "CMD !particle angryVillager {X} {Y} {Z} 2 2 2 0.1 20",
      "WAIT 1",
      "CMD !summon minecraft:lightning_bolt {X} {Y} {Z}",
      "CMD !particle angryVillager {X} {Y} {Z} 2 2 2 0.1 100",
      "WAIT 1",
      "CMD !summon minecraft:lightning_bolt {X_LOOK} {Y_LOOK} {Z_LOOK}",
      "WAIT 1",
      "GOTO 8 16",
      "CMD !summon minecraft:lightning_bolt {X_LOOK} {Y_LOOK} {Z_LOOK}",
      "PM {PLAYER} &l&dThunder just leave you..."
    ]
  }
```
Here, **"PM {PLAYER} &eThunder is with you"** have the **0** ID, **"CMD !summon minecraft:lightning_bolt {X_LOOK} {Y_LOOK} {Z_LOOK}"** have the **8** ID.
Each time you jump to next command, the counter increase, so while the counter is less than {COUNT_TIMIT} the goto will be apply, else, state will skip to the next instruction.<br>
  
**NeedToBeSaved** is a boolean that said, if at the server stopping, macros need to be saving (usefull if you have duration system with WAIT) or can be executed, ignoring time until finish them, before their deletion. <br>
  
In your example, **"GOTO 8 16"**, the instruction with **8** ID will be executed 4 times, the initial time, then 3 other times.
  
## Licenced server
  
Single licence: Frontier Pixelmon<br>
Network licence: None<br>
