# Modifiers
> Modifier tags  
> restartingStateRequired : The game must restart to make this modifier works.  
> recomputeUnitsRequired : Recompute all units when this modifier enabled or disabled.  
> clearNetRequired : Triggers a full update when this modifier enabled or disabled.  
> gameplayImpact : This modifier affect how the gameplay works. Modifiers with this tag are not allowed to be changed in mid game.  
> displayImpact : This modifier affect what can players see.  
> controllingImpact : This modifier affect how players control their units and their building queue. Modifiers with this tag are not allowed to be changed in mid game.  
> informingImpact : This modifier affect the ability of players know the stats of units and games. Modifiers with this tag are not allowed to be changed in mid game.  
> disallowStart : Starting a game that is not sandbox mode with enabled modifiers with this tag are not allowed.

## invalid
> tags: gameplayImpact  
> info: Allows unlimited usage of invlaid designs.

Allows units with any types of invalid with any amount in all game modes.

This is an extremely dangerous modifier. Use with cautious!

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

## cloak_not_attacked
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Units don't know how to attack cloaked units.

Remove cloaked enemies from weapons targeting of units.

## units_radius_ignore_occupied_cells
> tags: gameplayImpact, recomputeUnitsRequired  
> groups: vanilla_defects  
> info: Units radius will ignore occupied cells, only use center of parts.

The radius compute will only consider the center of parts rather than their occupied cells. This cause ships with same occupied cells nolonger have same raidus.

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

## weapons_disabled_inside_enemies
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Weapons cannot fire when they or their minrange inside enemies.

Enable an ill-designed weapon aim compute that cause weapons cannot fire when their min range (0m for most weapons) are beyond the target radius and inside the target.

## weapons_volley_overriden
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Weapons fire will clear their current volley.

Weapons like sidewinders and autocannon will cancel their queued bullets when fire.

The effect is only visible when such weapon has their reload time significantly reduced, and the only valid design to make this happen is autocannon with 4 or more reloaders.

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
> info: Disable manual control, only AI rules is allowed.

You cannot control units, units are exclusivly controlled by their AI. Useful when you want host an AI only race.

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

## no_friction
> tags: gameplayImpact  
> info: Real space that no friction.

Friction are disabled. This is a very wild modifier and units navigation cannot handle it, they will launch themselves out of their destination in a crazy speed.

## tripled_energy
> tags: gameplayImpact  
> info: Energy regeneration and transfer amounts are tripled.

Energy regen of units are tripled, and the transfer amount of energy transfer are tripled.

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

## missiles_retargeting
> tags: gameplayImpact  
> info: Missiles can find new target after target lost.

When missiles lose their target, they will lock down a new target, if any.

## missiles_smart_aim
> tags: gameplayImpact  
> info: Missiles can predict target movement.

Missiles will moving towards the destination of their target rather than the current location of their target.

## missiles_track_cloaked
> tags: gameplayImpact  
> info: missiles will track cloaked units.

Missiles track cloaked units, and hit them when target decloaked.

## missiles_full_arc
> tags: gameplayImpact  
> info: Tracking weapons can fire without needs of target in arc.

Tracking weapons can fire even if their target isn't in firing arc.

## orb_retargeting
> tags: gameplayImpact  
> info: Orbs from Orb launcher can fix their rotation after released from pods.

When Orbs released from their pods, they will target enemies and change their launch direction.

## energy_nosferatu_transfer
> tags: gameplayImpact  
> info: Energy transfer drains energy from enemies.

Energy transfer drains energy from enemies. In most cases this put enemies in a dead empty state that disabled to fire or move.

## stasis_field_hazard
> tags: gameplayImpact  
> info: A stasic field cover whole map that slow units, drains cloak and jump.

All ships are slowed and get their cloak and jump drained, just like what stasic field do.

## random_orb_fire_range
> tags: gameplayImpact  
> groups: vanilla_defects  
> info: Release time of orb spheres from Orb Launcher are back random.

The time of orb released from their pod become random.

## accurately_weapon_range
> tags: gameplayImpact, recomputeUnitsRequired  
> info: Weapons will fire with their range become more accurate.

Weapon will compute their true bullets travel range, and fire when enemies enter this range, rather than the range stat. This also makes the attack range of Orb Launcher become insanely long.

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

## flame_hazard
> tags: gameplayImpact  
> info: Units are fully burned upon build.

Burn value of units are set to their hp when they are built. This quickly drains hp from battleships. Shield ships are highly resist to this.

## ghost_fleet
> tags: gameplayImpact  
> info: Units are under a superior version of cloak upon build.

Units are cloaked upon build, and this cloak don't decay overtime, unless they are decloaked.

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

## shield_energy_usage_no_thershold
> tags: gameplayImpact  
> info: Shield energy usage has no thershold.

Remore the energy thershold for shields to working.

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

## cloak_hardened
> tags: gameplayImpact  
> info: Fire weapons will not decloak the ship doing it.

Cloaked units can fire weapons without decloak them.

## cloak_vulnerable
> tags: gameplayImpact  
> info: Cloaked ships are vulnerable to multihit and aoe.

Make cloaked units vulnerable to multihit bullets and aoe explosions.

## cloak_invulnerable
> tags: gameplayImpact  
> info: Cloaked ships are immune to all types of damage.

Cloaked units are immune to all types of damage, includes multihit, aoe, and burn damage. Their burn value still decay overtime despite not doing damage.

## cloak_disappeared
> tags: gameplayImpact, informingImpact  
> info: Cloaked unarmed units completely disappeared to enemies.

Cloaked unarmed units are completely disappeared to enemies. They are not shown on their screen, AI rules of enemies cannot trace them, and weapons of enemies won't attack them since they don't know these units exist.

## cloak_phenomena
> tags: gameplayImpact  
> info: All units cloak 21%/s overtime.

All units passively gains cloak at a rate of 21% of mass per second.

## hide_stats
> tags: displayImpact, informingImpact, clearNetRequired  
> info: Cannot see hp, energy and shield stats of units.

Hp, energy and shield stats of units are not shown to players, but they are still there.

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
