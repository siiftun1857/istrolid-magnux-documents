# Modifiers
> Modifier tags  
> restartingStateRequired : The game must restart to make this modifier works.  
> recomputeUnitsRequired : Recompute all units when this modifier enabled or disabled.  
> clearNetRequired : Triggers a full update when this modifier enabled or disabled.  
> gameplayImpact : This modifier affect how the gameplay works. Modifiers with this tag are not allowed to be changed in mid game.  
> displayImpact : This modifier affect what can players see.  
> controllingImpact : This modifier affect how players control their units and their building queue. Modifiers with this tag are not allowed to be changed in mid game.  
> informingImpact : This modifier affect the ability of players know the stats of units and games. Modifiers with this tag are not allowed to be changed in mid game.
> mapGeneratorImpact : This modifier affect how the map generator works.  
> disallowStart : Starting a game that is not sandbox mode with enabled modifiers with this tag are not allowed.

## invalid
> tags: gameplayImpact  
> info: Allows unlimited usage of invlaid designs.

Allows units with any types of invalid with any amount in all game modes.  
This is an extremely dangerous modifier. Use with cautious!

## generating_theme
> tags: mapGeneratorImpact  
> info: Map generator will generate theme and less rock.

The map generator will set the theme of the battlefield when the game starts.  
One or more types of rocks will be excluded from generating.

## weapons_aim_defects
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Weapons aim use 32x loop simpling instead of quadratic equation solver, do not computre arm delay effect, only aim target center, and aim closest edge point even if they or their minrange inside enemies.

By default the server use a quadratic equation solver to compute movement interception for weapon aim, which gives perfect accuracy, proper process both result of the equation, and great performance improvement. This modifier enables vanilla weapon aim, a loop simpling that check each 1/32 part of bullet life to find the least miss one.  
Weapons aim will assume the bullet fly towards their target immediately after fired, even if they don't.  
Weapons aim will always fire weapons at target's near edge, causing exact aoe weapons can be easily dodged by stopping the targeted unit.  
Weapons aim will not fire even if a part of the target is in arc, only consider target center is in arc.  
Enable an ill-designed weapon aim compute that cause weapons cannot fire when their min range (0m for most weapons) are beyond the target radius and inside the target.

## gamedev
> tags: recomputeUnitsRequired, clearNetRequired, gameplayImpact  
> incompatible_with: legacy_v4  
> info: Enable experimental indevelop game changes.

This modifier enable gamedev changes, includes shield absorb extra damage at cost of e drain.

## legacy_v49
> tags: recomputeUnitsRequired, clearNetRequired, gameplayImpact  
> incompatible_with: gamedev  
> info: Enable a legacy game config from beta version 49.

This modifier bring the game back to v49 behaviors, includes units center compute now use their mass center rather than parts center.

## kitebug
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Enables kitebug.

The kitebug is a bizarre interaction between pull and other weapons, especially Phase Bomb Launcher. It caused by pull giving very high burst velocity to an enemy, making the movement predication used by weapons consider the target is coming very soon but it does not, resulting other weapons fire too far away from the target, waste their energy, damage and cooldown.  
The server will make units not to be considered as faster than its maximum speed for weapons target purpose. This modifier will turn it off, return the kitebug to the game.

## overcost
> tags: gameplayImpact  
> info: Allows overcost design, with an extra cost penalty.

Overcost is allowed, but there is a penalty for doing it.  
A cost multiplier is applied to cost of all parts. The cost multiplier is 100% if not overcost, and for every 2% beyond the cost limit, the cost multiplier increase 1%.  
This means a unit with $2000 parts cost will cost $3000 to build, and a unit with $3000 parts cost will cost $6000 to build.

## supercapital_bridge
> tags: gameplayImpact  
> info: Allows supercapital bridge.

Having supercapital bridge on unit is nologer being considered as invalid.

## battleship_thruster
> tags: gameplayImpact  
> info: Allows battleship thruster.

Having battleship thruster on unit is nologer being considered as invalid.

## explosion_damage_delay
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Explosions do damage after 1 tick after their creation.

Explosions will not do damage at the tick they are created, their damage is delayed to the next tick.

## cloak_not_attacked
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Units don't know how to attack cloaked units.

Remove cloaked enemies from weapons targeting of units.

## cloak_initially_decloak
> tags: gameplayImpact  
> groups: vanilla_defects  
> incompatible_with: ghost_fleet  
> info: Cloaked units spawn with decloaked.

Units spawn without cloak, even if they are capable of cloaking.

## units_move_defects
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Units do not try to save energy and force for movement, result in waste of energy and move beyond destination.

Units can move beyon their destination, causing them spinning in a point and consistently waste energy and aim.

## units_idle_ai_target_2nd_closest
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Units idle ai will target the 2nd closest enemy if the closest enemy is cloaked.

If the closest enemy is cloaked, the idleAI of unit will target the next closest enemy, regardless this one is cloaked or not.

## units_radius_500m
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Units radius are at least 500m.

The min radius of a unit is now 500m, instead of 10m, or 20m with `units_radius_ignore_occupied_cells`.

## units_radius_smallest_circle
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Units center and radius will use the smallest circle.

The center and radius compute will use the smallest circle for endpoints of all parts.  
However, clients compute units center on their own, do not get it from the server, result in a visual weirdness issue.

## units_radius_ignore_occupied_cells
> tags: gameplayImpact, recomputeUnitsRequired  
> groups: vanilla_defects  
> info: Units radius will ignore occupied cells, only use center of parts.

The radius compute will only consider the center of parts rather than their occupied cells. This cause ships with same occupied cells nolonger have same raidus.

## units_radius_shield_render_larger
> tags: displayImpact  
> info: Shield render use expanded radius rather than using its true radius.

Enable the units shield rendering method that currently used by vanilla games.  
Enable this modifier will cause units shield expand by this formula:  
$$r_{after}={{2\sqrt{2}\times r_{before}+80\sqrt{2}}\over{3}}$$

## jump_maintain_energy_usage
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Jump engine acts as a negative regen generator.

Jump engines will keep consuming energy even if jump is already fully charged.

## weapons_hit_dead_entites
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Weapons will hit dead entites.

Bullets will hit dead units and instent weapons will fire at dead units.

## weapons_volley_overriden
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Weapons fire will clear their current volley.

Weapons like Sidewinders and Autocannon will cancel their queued bullets when fire, result in a waste of energy.  
The effect is only visible when such weapon has their reload time significantly reduced, and the only valid design to make this happen is Autocannon with 4 or more reloaders.

## sidewinder_volley_delay
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Sidewinder has a delay between two bullets in a volley.

Add an 1/16 second delay between bullets of a volley of Sidewinders. Without this modifier, Sidewinders will unload its entire volley at the same time.

## autocannon_volley_no_delay
> tags: gameplayImpact  
> info: Autocannon has no delay between bullets in a volley.

Remove the 1/8 second delay between bullets of a volley of Autocannon.

## units_collide_during_warpin
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Collision between new untis and old units are disabled.

Make all units collides at same strenght. Without this modifier, newly built units who have warp in flast on will have reduced collision with those who don't.

## units_ai_message
> tags: displayImpact  
> info: Shows AI messages.

Show AI messages when you select units. You will need to turn it on on your client too to make it work.

## cooperate
> tags: controllingImpact, clearNetRequired  
> info: Give players full control to all team units.

You have full control to all units belong to your team, which is exclusive to their builder without this modifier.  
You are allowed to do anything with units in your team, includes move, follow, stop, and self-destruct. Only enable this modifier if you trust your teammates.

## ai_only
> tags: controllingImpact  
> groups: ai_tournament  
> info: Disable manual control, only AI rules is allowed.

You cannot control units, units are exclusivly controlled by their AI. Useful when you want host an AI only race.

## ai_off
> tags: controllingImpact  
> groups: tournament, ai_tournament  
> info: Disable AI rules.

All ai rules are disabled, only manual controls.

## ai_player_disabled
> tags: gameplayImpact  
> groups: tournament  
> info: Disable AI players.

AI players are disabled. Enabling this modifier will kick all AI players.

## fleet_lock
> tags: controllingImpact  
> groups: tournament  
> info: Disable AI rules.

All ai rules are disabled, only manual controls.

## never_dead
> tags: disallowStart, gameplayImpact  
> info: Units will not die.

Units will not die even if their hp dropped to and below 0.

## ffa_sandbox
> tags: disallowStart, gameplayImpact  
> info: Enable free for all sandbox mode.

Team of units now are their builder. Units will attack all units that are not belong to the same builder.

## peaceful
> tags: disallowStart, gameplayImpact  
> info: Units will not attacking enemies.

Units will nolonger consider anything is their enemies.

## all_friendly
> tags: disallowStart, gameplayImpact  
> info: Units will help their enemies.

Units will consider anything is their allies, even if they are enemies at the same time. This cause energy transfer to charge them.

## random_filed_location
> tags:  gameplayImpact  
> groups: vanilla_defects  
> info: Units will be field at a random location in their spawn.

Fielded units will appear at a random location in spawn, rather than the centre of their spawn.

## random_ai_rule_detals
> tags:  gameplayImpact  
> groups: vanilla_defects  
> info: Units ai rules will use randomness.

AI rules will use random generator to determine their behavior, resulting different actions taken in the same situation.

## 1k_builder
> tags: gameplayImpact  
> info: Units building cost $1000 each time, and build the most possible amount of units in $1000.

Field a unit always cost $1000, and the amount of fielded units is the maximum amount allowed in $1000. This makes units cost just above $500 become a waste of money and units cost more than $1000 cannot be fielded.

## instant_capture
> tags: gameplayImpact  
> info: Touching an unguarded command point will instantly capture it.

The capture time of command points are reduced to 0 sec.

## half_friction
> tags: gameplayImpact  
> info: Half friction, doubled maximum speed.

Friction are cut in half, this makes maximum speed of all units twice.

## one_third_friction
> tags: gameplayImpact  
> info: 1/3 friction, tripled maximum speed.

Friction are cut in third, this makes maximum speed of all units thrice.

## no_friction
> tags: gameplayImpact  
> info: Real space that no friction.

Friction are disabled. This is a very wild modifier and units navigation cannot handle it, they will launch themselves out of their destination in a crazy speed.

## tripled_hp
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Units raw HP amount are tripled.

HP of units are tripled.

## tripled_energy_capacity
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Units energy capacity are tripled.

Energy capacity of units are tripled.

## tripled_energy_generating
> tags: gameplayImpact  
> info: Energy regeneration and transfer amounts are tripled.

Energy regen of units are tripled, and the transfer amount of energy transfer are tripled.

## tripled_shield_capacity
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Units shield capacity are tripled.

Shield capacity of units are tripled.

## tripled_shield_generating
> tags: gameplayImpact  
> info: Shield regeneration amounts and energy usage are tripled.

Shield regen of units are tripled, while energy cost per shield HP generated are the same.

## infinity_energy
> tags: gameplayImpact  
> info: Units has infinity energy to use.

Energy of units are set to infinity. This also allows operating units with no energy storage.

## no_base_gen_energy
> tags: gameplayImpact  
> info: Remove basic 40E/s regen of units.

The basic 40E/s energy regen of units are removed, and this can cause a dead empty state for ships without a reactor or solar. Also making ships without energy regen immune to EMP stun effect.

## units_collide_hardened
> tags: gameplayImpact  
> info: Collision between untis are hardened.

Collision between untis are hardened and it is almost impossible to make a unit go through others.

## units_collide_disable
> tags: gameplayImpact  
> info: Collision between untis are disabled.

Collision between untis are disabled, and any amount of units can stack in the same location.

## instant_turn
> tags: gameplayImpact  
> info: Turn action are complete immediately.

Turning speed of units are set to infinity deg/s, making them finish turning instantly even for largest battleships.

## tripled_unarmed
> tags: gameplayImpact  
> info: Parts of unarmed units are tripled.

All parts of units without any weapons are tripled, while the cost to build them isn't changed.

## hpd_singlehit
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Heavy pd bullets are destroyed upon hitting any unit.

Heavy PD bullets are set to dead when they hit any unit, rather than using the "remaining damage" mechanic.

## hpd_deadhit
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Dead heavy pd bullets can still hit things.

Heavy PD bullets can hit things even if they are set to dead.

## hpd_multihit
> tags: gameplayImpact  
> info: Allows heavy pd bullet hit multiple units.

Heavy PD bullets will pass through units to hit multiple units.

## tesla_hits_missiles
> tags: gameplayImpact  
> info: Tesla now hits missiles.

Tesla will now fire and arc nearby missiles to destroy them.

## flak_hits_missiles
> tags: gameplayImpact  
> info: Flak cannon now hits missiles.

Flak bullets will delete all missiles in its blast area.

## sidewinder_hits_missiles
> tags: gameplayImpact  
> info: Sidewinder now hits missiles.

Sidewinders now engage hostile missiles to ram and destroy them.

## sidewinder_extended_retargeting
> tags: gameplayImpact  
> info: Sidewinder retargeting enemies in futher distance.

Sidewinder retargeting range increased by its remaining travel range from a static 1500m, and also try retargeting every tick instead of every 4 tick.

## remove_minimum_range
> tags: gameplayImpact  
> info: Remove minimum range of Artillery Gun and Orb Launcher.

The minimum fire range of Artillery Gun and Orb Launcher are removed.  
For the Artillery Gun, it can instantly hit anything close to it. For Orb Launcher, the orb can fly beyond the target and then can't hit them.

## self_push_pull_waves
> tags: gameplayImpact  
> incompatible_with: bothway_push_pull_waves, mass_versus_push_pull_waves  
> info: Pulles and pushes are applied on units fire them.

When pulls and pushes hit units, the unit fire them are pulled or pushed, and the unit get hit isn't affected. Damage of these bullets still applied to units they hit.

## bothway_push_pull_waves
> tags: gameplayImpact  
> incompatible_with: self_push_pull_waves, mass_versus_push_pull_waves  
> info: Half power of pulles and pushes are applied on units fire them.

When pulls and pushes hit units, the unit fire them are pulled or pushed for 50% strength, and the unit get hit are pulled or pushed for 50% strength.

## mass_versus_push_pull_waves
> tags: gameplayImpact  
> incompatible_with: self_push_pull_waves, bothway_push_pull_waves  
> info: Power of pulles and pushes are applied on both units get hit and units fire them.

When pulls and pushes hit units, both the unit fire them and the unit get hit are pulled or pushed, and the strength is based on their mass, lighter ships are affected more than heavy ships.

## push_pull_waves_force_hit_per_tick
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Bullets of pulles and pushes apply their force effect every tick even if they did it to a target before.

Pull and push bullets will apply their force effect as long as they are touching an enemy, even if they have been hit before. 

## push_pull_waves_no_instant_pinning
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Bullets of pulles and pushes will not repeatedly apply their force effect until the target has velocity towards force direction.

Pull and push bullets will not repeatedly apply their force effect until the target has velocity towards force direction.

## push_pull_waves_no_stack
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Bullets of pulles and pushes can cancel force effect even if they did not hit the target before.
 
Push and push bullets will cancel force effect if target has velocity towards force direction, even if they never do the effect to the target before, causing stacking pulls or pushs cancel each other.

## weapons_finite_turn
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Weapons turn rate is limited to 916.732 deg/sec.
 
Weapons now have a 916.732 deg/sec turn rate, makes them cannot immediately fire at something behind their current facing direction.

## orb_no_delay
> tags: gameplayImpact  
> info: Orb has no arm delay.

Orbs will skip their 2.5625-second arm delay and immediately fly towards their target.

## phase_bomb_no_delay
> tags: gameplayImpact  
> info: Phase bomb has no arm delay.

Phase Bombs will skip their 1.75-second arm delay and immediately fly towards their target.

## missiles_retargeting
> tags: gameplayImpact  
> info: Missiles can find new target after target lost.

When missiles lose their target, they will lock down a new target, if any.

## missiles_smart_aim
> tags: gameplayImpact  
> info: Missiles can predict target movement.

Missiles will moving towards the destination of their target rather than the current location of their target.

## missiles_avoid_hpd
> tags: gameplayImpact  
> info: Missiles can dodge HPD bullets.

Missiles will actively moving to dodge incoming point defence bullets, includes HPD bullets, and Flak bullets if `flak_hits_missiles` is on, and Sidewinder bullets if `sidewinder_hits_missiles` is on.

## missiles_track_cloaked
> tags: gameplayImpact  
> info: missiles will track cloaked units.

Missiles track cloaked units, and hit them when target decloaked.

## missiles_full_arc
> tags: gameplayImpact  
> info: Tracking weapons can fire without needs of target in arc.

Tracking weapons can fire even if their target isn't in firing arc.

## missiles_stop_friction
> tags: gameplayImpact  
> info: Missiles are affected by stop friction.

Missiles will be affected by inertia and stop friction like units do.

## orb_retargeting
> tags: gameplayImpact  
> info: Orbs from Orb launcher can fix their rotation after released from pods.

When Orbs released from their pods, they will target enemies and change their launch direction.

## orb_defects
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Orbs from Orb launcher have random stage time and can overshoot an extremely long range.

Make overshoot range of Orbs extended by bullet speed mods.  
The time of orb released from their pod become random.

## no_overshoot
> tags: gameplayImpact  
> info: Set overshoot stat of all weapons to 0%.

Completely disable the overshoot mechanic, bullets will instantly vanish upon passing their maximum range.

## no_overshoot_decay
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Overshooted bullets nolonger have their damage reduced.

Make bullets do full damage in their overshooted range.

## weapons_full_arc
> tags: gameplayImpact, recomputeUnitsRequired  
> info: All weapons have 360 firing arc.

All turrets can shoot any directions.

## weapons_no_reload
> tags: gameplayImpact  
> info: All weapons do not reload.

Weapons reload time is reduced to 1 tick (0.06 second).

## energy_nosferatu_transfer
> tags: gameplayImpact  
> info: Energy transfer drains energy from enemies.

Energy transfer drains energy from enemies. In most cases this put enemies in a dead empty state that disabled to fire or move.

## energy_transfer_infinity_range
> tags: gameplayImpact  
> info: Energy transfer has infinity operate range.

Energy transfer do not have an operation range limit, charge all allies. With `energy_nosferatu_transfer`, they also drain all enemies.

## energy_transfer_thershold
> tags: gameplayImpact  
> info: Energy transfer will not darin the user to below 1 second of generation or 50% capacity, whatever one is lower.

Energy transfer do not drain the user's energy to below the value equal to 1 second of energy regen or 50% energy capacity, depending which one is lower.


## stasis_field_hazard
> tags: gameplayImpact  
> info: A stasic field cover whole map that slow units, drains cloak and jump.

All ships are slowed and get their cloak and jump drained, just like what stasic field do.

## stasis_field_superior
> tags: gameplayImpact  
> info: Stasis field affected units instantly lose all cloak and jump.

Ships affected by tasic field effect will instantly lose all cloak and jump, instead of slowly drained.

## random_energy_transfer_target
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: The order to share energy with energy transfer are random.

Energy tranfer will randomly choose their share target instead of prioritize low energy allies first.

## random_machine_gun_spread
> tags: gameplayImpact  
> info: Spread of Machine Gun are back random.

Enable random spread for Machine Gun, which are disabled without this modifier.

## random_sniper_gun_fire_interval
> tags: gameplayImpact  
> info: Fire interval of Sniper Gun are back random.

Enable random fire interval for Sniper Gun, which are disabled without this modifier.

## sniper_gun_fire_no_move
> tags: gameplayImpact  
> info: Standing still is required to fire Sniper Gun.

Enable no movement requirement for Sniper Gun, which are disabled without this modifier.

## accurately_weapon_range
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Weapons will fire with their range become more accurate.

Weapons will compute their true bullets travel range, and fire when enemies enter this range, rather than the range stat. This also makes the attack range of Orb Launcher become insanely long if `orb_overshoot` is enabled.

## infinity_weapon_range
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Weapons have infinity range.

Weapons have infinity range, their bullets can travel forever and instant weapons can damage enemies at any range.

## mods_one_free_share
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Weapon mods share count are being considered 1 less.

The share count of weapon mods are considered 1 less, this means there is no penalty to mods effect when they are shared to 1 or 2 weapons, and the penalty is equal to shared to 2 weapons when it shared to 3 weapons.

## mods_twiced
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Weapon mods are applied twice.

The stats changes of weapon mods are applied twice, making them way more powerful. Note this will also apply their stats penalty twice, cause their reload time become even longer or cost more energy to fire. Affects snipal turrel mounts too.

## mods_energy_than_reload
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Weapon mods that increase reload time now increase energy per shot instead.

Negative reload time bouns of all weapon mods now affect energy per shot instead. This means there are no reload penalty from weapon mods at all.

## mods_increased_share_penalty
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Weapon mods share penalty increased to 25% from 15%.

Share weapon mods now suffer a heavier penalty, 25% per share rather than 15% per share.

## mods_no_share_penalty
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Removes weapon mods share penalty.

Share weapon mods do not come with penalty.

## mods_no_flat_range
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Removes the flat range bonus from Weapon mods.

Remove flat range bonus from Targeting Subsystem and Speed Coils.

## mods_spinal_advanced
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Spinal Turret Mound improves all weapon stats slightly.

Enables weapons modifiers of Spinal Turret Mound from gamedev.

## flame_hazard
> tags: gameplayImpact  
> info: Units are fully burned upon build.

Burn value of units are set to their hp when they are built. This quickly drains hp from battleships. Shield ships are highly resist to this.

## ghost_fleet
> tags: gameplayImpact  
> info: Units are under a superior version of cloak upon build.

Units are cloaked upon build, and this cloak don't decay overtime, unless they are decloaked.

## warhead_detonate_delay
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Warheads detonate delayed 1 tick.

Warheads explode in post death instead of in the tick they are triggered.

## warhead_disable
> tags: gameplayImpact  
> info: Warheads will not explode.

Warheads will not explode at all, making them useless.

## stupid_fire
> tags: gameplayImpact  
> info: Weapons will fire even if they can't hit target.

Weapons will fire at enemies even if they are out of their range. Doesn't affect instant weapons and exact hit aoe weapons.

## burn_unlimited
> tags: gameplayImpact  
> info: Burn amount on a unit has no limit.

Burn of units can be applied to beyond their hp.

## burn_limited
> tags: gameplayImpact  
> info: Burn amount on a unit is limited to remaining hp of it.

Burn of units will be reduced to their current hp if they take damage from other source.

## instant_burn
> tags: gameplayImpact  
> info: Burn damage are 100% applied immediately.

100% burn damage are applied every tick, rather than 3% per second.

## emp_unlimited
> tags: gameplayImpact  
> info: EMP stun time is unlimited.

There are no minimum limit of energy and the stun effect duration from EMP are extended to infinity.

## emp_stun_disabled
> tags: gameplayImpact  
> info: EMP stun disabled.

EMP damage cannot cause stun effect i.e. reducing energy to negative value.

## shield_energy_usage_no_thershold
> tags: gameplayImpact  
> info: Shield energy usage has no thershold.

Remove the energy thershold for shields to working.

## shield_ineffective
> tags: gameplayImpact  
> info: Shield do not block damage.

Make shield not blocking damage, effectively nullified them.

## charger_heal_stun
> tags: gameplayImpact  
> info: Chargers can charge stunned ships.

Energy Transfer can charge units with negative energy, i.e. units stunned to enemies EMP.

## fragile
> tags: gameplayImpact, displayImpact, clearNetRequired  
> info: Units will be one shot to death.

Units are killed when they recieved any damage.

## cloak_attacked
> tags: gameplayImpact  
> info: All weapons will engage cloak regardless they can hit cloak or not. Instant weapons are not affected.

Remove invulnerable check of weapons targeting system, they will try fire projectiles at cloaked units. This modifier has no effect to instant weapon since they only do guaranteed hits.

## cloak_disruptable
> tags: gameplayImpact  
> info: Weapons that can hit cloaked units will also decloak them.

Any bullets that can hit cloaked units will decloak them when they do damage.

## cloak_units_collide_disable
> tags: gameplayImpact  
> info: Collision between cloaked untis are disabled.

Collision between cloaked untis are disabled, allowing them stack in the same location.

## cloak_units_no_decloak
> tags: gameplayImpact  
> info: Cloaked units cannot decloak cloaked enemies, unless they have stasis field equipped.

Cloaked units cannot decloak enemies.

## cloak_advanced
> tags: gameplayImpact  
> info: Fire weapons will not decloak the ship doing it.

Cloaked units can fire weapons without decloak them.

## cloak_hardened
> tags: gameplayImpact  
> info: Cloaked ships cannot be decloak by close to enemies.

Decloak enemies by stay in 100m to it is disabled.  
Cloaked units can still be decloaked by stasis, cloak decay overtime, or fire weapon.

## cloak_vulnerable
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Cloaked ships are vulnerable to multihit and aoe.

Make cloaked units vulnerable to multihit bullets and aoe explosions.

## cloak_disappeared
> tags: gameplayImpact, informingImpact  
> info: Cloaked unarmed units completely disappeared to enemies.

Cloaked unarmed units are completely disappeared to enemies. They are not shown on their screen, AI rules of enemies cannot trace them, and weapons of enemies won't attack them since they don't know these units exist.

## cloak_phenomena
> tags: gameplayImpact  
> info: All units cloak 21%/s overtime.

All units passively gains cloak at a rate of 21% of mass per second.

## heavy_beam_healing
> tags: gameplayImpact  
> info: Heavy beams can repair friendly units.

Heavy Beam turrets now capable of shooting allies to repair them, increasing hp equal to their damage, and overheal can reduce burn amount.  
They still capable of shooting enemies to do damage.

## instant_weapons_hits_cloak
> tags: gameplayImpact  
> info: Instant weapons can hit cloaked units.

Make cloaked units vulnerable to instant weapons. Tesla bolts cannot bounce to cloaked units without `tesla_bounce_cloak`.

## tesla_hits_cloak
> tags: gameplayImpact  
> info: Tesla bolts can hit cloaked units.

Make cloaked units vulnerable to Tesla turrets. Tesla bolts cannot bounce to cloaked units without `tesla_bounce_cloak`.

## tesla_bounce_cloak
> tags: gameplayImpact  
> info: Tesla bolts can bounce to cloaked units.

Tesla bolts can bounce to cloaked units. Tesla turrets cannot attack cloaked units directly without `instant_weapons_hits_cloak` or `tesla_hits_cloak`.

## tesla_bounce_unlimited
> tags: gameplayImpact  
> info: Tesla bolts can bounce unlimited amount of units.

Tesla bolts can bounce to any amount of units, instead of up to 10 units.

## jump_no_minjump
> tags: gameplayImpact  
> info: Jump engines do not have min jump distance.

Remove the min jump to jump.

## jump_auto_turn
> tags: gameplayImpact  
> info: Jump engines will automatically issue a jump move for burst turn.

When a unit with jump is turning, it will jump to instantly finish the turn, save the time.

## jump_auto_move
> tags: gameplayImpact  
> info: Jump engines will automatically issue a jump move when jump is fully charged.

When jump is fully charged and the unit is moving, it will jump to shorten the trip.

## weapons_velocity_inheritance
> tags: gameplayImpact  
> info: Bullets gain velocity from their caster.

When a bullet is created, its velocity adds the velocity of the unit fired it.

## no_sidewinder
> tags: gameplayImpact  
> info: Disallow usages of Sidewinder.

Invalidate unit designs if they have Sidewinder equipped.

## hide_stats
> tags: displayImpact, informingImpact, clearNetRequired  
> info: Cannot see hp, energy and shield stats of units.

Hp, energy and shield stats of units are not shown to players, but they are still there.

## hide_bullets
> tags: displayImpact, informingImpact, clearNetRequired  
> info: Cannot see bullets.

Bullets are not shown to players, but they are still there, and units with avoid bullets ai can still avoid them, and PD turrets still shoot bullets normally.

## look_up
> tags: displayImpact, clearNetRequired  
> info: Everything will look up.

Rotation of everything are set to 0 when they are displayed on clients. Doesn't affect their true rotation.

## chao_spin_unit
> tags: displayImpact, clearNetRequired  
> info: Every unit will spin.

Units will spinning on clients. Doesn't affect their true rotation.

## chao_spin_bullet
> tags: displayImpact, clearNetRequired  
> info: Every bullet will spin.

Bullets will spinning on clients. Doesn't affect their true rotation.

## dock_to_100grid
> tags: displayImpact, clearNetRequired  
> info: Position of everything are multiples of 100.

Position of everything are set to multiples of 100 on clients. Doesn't affect their true position.

## no_rock
> tags: displayImpact  
> groups: tournament  
> info: Erase all rocks, structures, debrees, clouds from the map.

Remove all flavor objects from the map, only things related to combat left.

## burn_effect
> tags: displayImpact  
> info: Units have burning visul effects.

Units are visually burning, but are not buring actually (unless they get attacked by real flame).

## flash_off
> tags: displayImpact  
> info: Turn off units destruction flash.

Units will nolonger flash when they are destroyed.

## warp_enter
> tags: displayImpact  
> info: A very cool units FTL enter effect.

Units warps into the battlefield rather than assembled.

## top_out
> tags: displayImpact  
> info: A very cool death effect that dead units top out from map.

Destroyed units fly upwards, throws their wrecks in the same direction.

## hide_mouse
> tags: displayImpact  
> groups: tournament  
> info: Hide players mouse.

Remove the mouse display that informs players about others focus and actions.
