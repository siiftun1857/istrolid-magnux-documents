# Chat commands
## help
> Usage: !help \<command\>  

`<command>`: the command you need help.

Shows this page.  

## lang
> Usage: !lang \<lang\>  

`<lang>`: the language code you choose.

Make all messages from the server that are said to you using the language you choose.  
You can check the translation project of Magnux at <https://crowdin.com/project/istrolid-magnux>.  

## seed
> Usage: !seed  

Report the seed of current generated map.

## build
> Usage: !build \<slot num\> [count]  

`<slot num>`: The slot that holding the unit you want to build, between 1 and 10.  
`[count]`: The amount of units you want to build. Default to 1. Negative number dequeue builds.  

Queue or dequeue your building requests.

## jump
> Usage: !jump

Finish the movement action of selected units that you have control to, by a jumping action.  
Only works in sandbox.

## side
> Usage: !side \<alpha|beta|spectators\>  
> Alias: join  
> Require waiting state  

`<alpha|beta|spectators>`: The team you want to join.  

Set your own team. Useful if the team has 3 or more players where your client won't show "join this team" button.

## mode
> Usage: !mode \<server type\>  
> Exclusive to host  
> Require waiting state  

`<server type>`: The new server type you want.  

Set the server type to the given value, it applied when the game started.  
Valid server types are `sandbox`, `conquest`, `deathmatch`, `blitz`, `survival`.  

## start
> Usage: !start [-S|-E] [seed]  
> Exclusive to host  
> Require waiting state  

`-S` flag: When starting a sandbox, force a small map.  
`-E` flag: When starting a sandbox, force an empty map.  
`[seed]`: The seed to generate the map.  

Try to start the game with the given seed and option.  
This set a 6 sec countdown which can be aborted.  

## givehost
> Usage: !givehost \<new host name\>  
> Exclusive to host  

`<new host name>`: The player to become new host.  

Set the specific player to host. This remove your own host role.  

## shuffle
> Usage: !shuffle  
> Exclusive to host  
> Require waiting state  

Shuffle all players. Amount of players in each team aren't changed.  
Rare cases may occur that shuffle all players to where they were, making it shuffled but not shuffled.  

## simrate
> Usage: !simrate \<multi\>  
> Exclusive to host  

`<multi>`: Multiply of normal speed, with 1 is the normal speed. Must between 0.5 and 10.  

Set the speed of the game.

## theme
> Usage: Usage: !theme \<theme\>  
> Exclusive to host  

`<theme>`: The theme you want to use.  

Set the theme of the game.  
Valid themes are `main`, `grayblue`, `orange_legacy`, `blue`, `fadered_legacy`, `fadered`, `tealwhite`, `whitepurple`, `darkness`, `moonyellow`, `pinkpurple`, `greenbrown`, `bluebrown`, `tealorange_legacy`, `greenpurple`, `lemondarkred`, `lemondarkred_legacy`, `tanslate`, `redgreen_legacy`, `yellowpuce`, `yellowpuce_legacy`, `yellowcyan`, `puredarkness`, `purebrightness`, `galaxy`.  

## players
> Usage: !players   

Print all players in the server.  

## recolorai
> Usage: !recolorai \<color\> [player number ...]   

`<color>`: A hex color, it can start with or without #.  
`[player number ...] `: Specific players to recolor, split with space to put mutliple numbers.  

Change the player color of AI players.  
You can get player number via !players command.  
Run recolorai without player number given will change all your AI players.  

## modifiers
> Usage: !modifiers [\<enable|disable|invert|info\> \<modifiers ...\>|reset|list]  

`modifiers enable ...`: Enable modifiers.  
`modifiers disable ...`: Disable modifiers.  
`modifiers invert ...`: Enable disabled modifiers, disable enabled modifiers.  
`modifiers info ...`: Get modifiers breif info.  
`modifiers reset`: Reset all modifiers to disabled state.  
`modifiers list`: Print a list of all enabled and disabled modifiers.  
`<modifiers ...>`: Modifiers you want to operate, split with space to put mutliple modifiers at the same time.  

The modifiers system is one of the signature ability of Magnux that allows players change game behaviors in many different ways.  
For more detals of modifiers, check [Modifiers Document](https://github.com/siiftun1857/istrolid-magnux-documents/blob/master/modifiers.md).
