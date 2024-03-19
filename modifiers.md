
## orb_overshoot
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Orbs from Orb launcher can overshoot an extremely long range.

Make overshoot range of Orbs extended by bullet speed mods.

## random_orb_fire_range
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Release time of orb spheres from Orb Launcher are back random.

The time of orb released from their pod become random.

## cloak_invulnerable
> tags: gameplayImpact  
> info: Cloaked ships are immune to all types of damage.

Cloaked units are immune to all types of damage, includes multihit, aoe, and burn damage. Their burn value still decay overtime despite not doing damage.

## weapons_disabled_inside_enemies
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Weapons cannot fire when they or their minrange inside enemies.

Enable an ill-designed weapon aim compute that cause weapons cannot fire when their min range (0m for most weapons) are beyond the target radius and inside the target.

## weapon_aim_loop_simpling
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Weapons aim use 32x loop simpling, instead of quadratic equation solver.

By default the server use a quadratic equation solver to compute movement interception for weapon aim, which gives perfect accuracy, proper process both result of the equation, and great performance improvement.  
This modifier enables vanilla weapon aim, a loop simpling that check each 1/32 part of bullet life to find the least miss one.

## weapon_aim_ignore_arm_delay
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Weapons aim do not computre arm delay effect.

Weapons aim will assume the bullet fly towards their target immediately after fired, even if they don't.

## weapon_aim_no_steady_aoe
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Weapons always aim the near edge of the target.

Weapons aim will always fire weapons at target's near edge, causing Phase Bomb can be easily dodged by stopping the targeted unit.
