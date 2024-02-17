# Magnux changes
May not the full list.

## Server instance
### Chat commands
The server offers chat commands. For more detals of it, check [Chatcmds Document](https://github.com/siiftun1857/istrolid-magnux-documents/blob/master/chatcmds.md).

### Tick rate Stabilizer
The server uses its own loop body implement to run sim.simulate. On each tick, the "last tick time" will subtract the interval time of each tick instead of setting the "last tick time" to the current time.  
Once "last tick time" is 1000ms behind current time after a tick started, it will set it to 1000ms behind current time, remove values added to "dropped time" and issue an "Can't keep up!" alarm.  
Once "dropped time" reaches 15000ms in sandbox or 90000ms in other modes, the server will restart to recover from the extreme tick rate dropping event.  
Completing a tick with spare time will reduce "dropped time".

### Player check queue
The server uses an async player check that, unlike other servers, only creates a player instance in Sim after the player is checked and is valid. This prevents attacks that try to run malicious commands before the connection is killed by player check fail.

### Network data validity check
The server will check if incoming network data are valid in data type; if not, they are ignored.

### Replay recorder
The server records and generates replay files for every game played.

### Sim restart
The sim instance can be replaced on the server. This can be manually issued by a server administrator, or automatically by the server when the server is idle. In very rare occurrences, if sim crashes, a new sim is generated too.  
When sim is restarted, players are automatically passed to the new sim, no reconnect is needed.

### Script reloader
A server administrator can hot reload changes to sim scripts, and restart the sim to apply them, without disconnecting players.

## Sim essential
### Modifiers
The modifeirs system (internally "feature flags") can change the game in many different ways.  
For more detals of modifiers, check [Modifiers Document](https://github.com/siiftun1857/istrolid-magnux-documents/blob/master/modifiers.md).

### Sim send data per player
The sim.send is remade to be able to generate and send data for each player.  
Only player who issued full update get the full update data.  
Some modifiers can change to send different data to each player.

### Players management
Players join do not remove disconnected players.  
After a game started, disconnected players are cleared from the server.

## Sim map
### Map generating
Map generator use seed, and report seed after a game. Start with a seed is possible.  
Map generating generates points layout before flavor objects.  
Spawn y-pos is fixed at 0.  
By default, all four types of flavor objects are generated.

### Theme
Theme can be manually changed. By default map generating does not change theme.

## Sim players
### Build queue limit
Build queue length cannot go beyond 1000.

### Full update rate limit
Issue full update requests too often will cause the server refuse to send any data for few seconds.  
This rate limit is unlikely to reach if not using a script to do it. 

## Sim ai
### Closest cache
Units AI builds a closest cache to shorten the amount of time needed for thing finding, at cost of memory usage.

### No random AI detals
Units AI will be executed in the order of they build, instead of a random order.  
AI rules do not add randomness to order destination.  
Field rules do not add random value to queue priority.  
"wiggle" rules are skipped.

### Performance data
The server has its own timer tree to track performance data. Performance data is included in network data by default.

## Sim players
### Realtime income
Players get income every tick. Income rate still the same.

### Queue of build queue
When players order units, they are added to "queue of build queue".  
Every 16 ticks the sim move all orders from "queue of build queue" to "build queue".  
Build queue runs every tick instead of every 16 ticks.

### Fixed spawn location
New units will be placed in the center of a spawn, instead of a random point in the spawn.

## Sim things
### Conquest
There are no "1v1" "2v2" "3v3" mode to pick. Start conquest games will automatically set the game mode name depending on players in the game.

### IFF
Things in sim have a dedicated IFF system. This allows them to use more advanced teaming behaviors instead of only considering the same side as allies and others as enemies.  
The IFF system works identical to "considering the same side as allies and others as enemies" if no modifiers are changing this.

### Extended range of find in range
If there are any units with radius more than 500m, range of "find in range" are expanded too.

### Map boundary
Map boundary on the server is a circle with 20km diameter, instead of a square with 40km length.  
Units cannot go beyond map boundary, and bullets go beyond it more than 500m are deleted.

### Speed limit
Speed of a thing cannot go beyond 480,000 m/s.

## Sim bullets
### Bullets ignore dead units
Bullets ignore dead units.

### HPD remaining damage
Dead HPD do not damage units.  
If HPD bullet do damage to a unit with HP below its "remaining damage", the "remaining damage" will be reduced by the HP and the bullet keep flying to hit next thing.

### Push and pull hits once
Push and pull bullet will only hit a target once.  
Push and pull bullet will apply force regardless target speed.

### Orb2
Orbs will enters their 2nd stage exactly at their minimum range, i.e. in 51 ticks, and do an effectively 41 ticks arm delay.  
Orbs do not add extra 24 ticks to their max life, making them do not overshoot an extreme range with speedcoils.

### Overshooted damage decay
Bullets do reduced damage in their overshooted range, linearly from 100% damage at 100% range, to 0% damage at 100% range + 100% overshooted range.  
Sidewinder bullets are the sole exception that do decay linearly from 100% damage at 150% range, to 0% damage at 225% range.  

## Sim units
### Radius compute
The radius compute considers the unit's occupied cells instead of the center of the parts. This means units with the same occupied cells have the same raidus. Additionally, unit radius can larger than 500m.

### Radius rendering
In vanilla games, unit shields are expanded by this formula:

$$r_{rendering}={{2\sqrt{2}\times r_{collision}+80\sqrt{2}}\over{3}}$$

This is not happening on the server, as unit shield radius rendering is perfectly accurate.

### Collision
Collision push direction is reversed for units in the exact pos in beta team.  
Units have reduced collision with other units with different "warp in" value than itself.

### Engines usage
When the unit is moving, it sorts its engines by energy efficiency, prioritizing engines with high thrust per energy cost.  
This means that a unit with hybrid engine types and low energy will always do the most thrust with limited energy.

### Weapons engagements
Instant weapons will not fire if the target is dead. Affected weapons includes Light Beam, Heavy Beam, Tesla Turret, Point Defence.  
Weapons will fire if can damage the target. This allows Artillery Gun, Heavy Flak, Phase Bomb Launcher, Gravity Pull Wave, Gravity Push Wave, Flamethrower engage cloaked targets if cloak vulnerable to these weapons are enabled.  
If a weapons minimum range is beyond target near radius, but not beyond their far radius, weapons will fire at their min range. Affected weapons includes Artillery Gun and Orb Launcher.  
Weapons aim will consider their arm delay, if they have. Affected weapons includes Phase bomb with a 1.75sec arm delay, and Orb Launcher with a effectively 2.5625sec arm delay.  
If any weapons fired and decloaked the user, sim will loop all weapons fire attempt again to find if there are any new decloaked units, allowing units who doesn't fire before to kill the new available target.

### Resources allocator
Cloak Generator, Shield Generator, Jump Engine use a resources allocator to use energy and generate their resources.  
If their resource generate per tick is below remaining amout to maximum, then it use reduced energy to generate reduced amount of resource; If their energy use per tick is above remaining energy, then it generate reduced amount of resource with remaining energy.

### Tick actions
Units tick are cycles in an order:
1. Units regain energy and cloak decay
2. Stasis Field and Jump Engine destabilize user's cloak
3. Cloak Generator generate cloak if user isn't cloaked
4. Warhead try explode, Stasis Field try affect enemies
5. Weapons try fire, and if any weapon fire decloaked user, loop again all weapons that skipped cloaked targets on new decloaked targets
6. Move, as well as everything else move
7. Cloak Generator, Shield Generator, Jump Engine generate cloak, shield, jump
8. Energy Transfer, burn decay, add energy overcharged from previous stages
10. Finish off dead units

### Cloak decay
Cloak decay runs every tick.

### Burn decay
Burn decay runs every tick, and will not reduce units HP to below 4.

### Energy Transfer
Energy Transfer will prioritize low energy allies first, instead of randomly choose transfer target.  
Energy Transfer runs every tick.

### No kitebug
The kitebug is a bizarre interaction between pull and other weapons, especially Phase Bomb Launcher. It caused by pull giving very high burst velocity to an enemy, making the movement predication used by weapons consider the target is coming very soon but it does not, resulting other weapons fire too far away from the target, waste their energy, damage and cooldown.  
The server will make units not to be considered as faster than its maximum speed for weapons target purpose.

### Weapons volley
Sidewinder and Autocannon will add bullets to fire to a "volley" storage.  
Even if these weapons fired again before another volley finished, they will not cancel other volleys.

### Sidewinder no volley delay
Sidewinder volley delay is 0 tick instead of 1 tick.
