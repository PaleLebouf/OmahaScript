<style type='text/css'>
ul {list-style-type: none;padding: 0;overflow: hidden;background-color: #333;}
li {  display:block; float: left;}
li a {display: block; color: white; text-align: center; padding: 14px 16px; text-decoration: none;}
li a:hover:not(.active) {background-color: #111;}
.active {background-color: #ffcc00;} </style>
<ul>
      <li><a href="https://palelebouf.github.io/OmahaScript/">Home</a></li>
      <li><a href="https://palelebouf.github.io/OmahaScript/megalo/docHome">Megalo Documentation</a></li>
      <li><a class="active" href="https://palelebouf.github.io/OmahaScript/megalo/qna">Megalo QnA</a></li>
</ul>
# Megalo QnA
This is a QnA answered by Bungie employee [Jon Cable](https://www.linkedin.com/in/jon-cable-941a6a4), one of the sandbox engineers at bungie who concieved of Megalo. The old halo.bungie.org forum website post is accessible [here](http://forums.bungie.org/halo/archive37.pl?read=1101488).

> What programming language does Megalo most imitate? Is it C-like or Python-esque?

None that I know of. It's kind of like BASIC without any functions or gotos, and the entire program is run once every game tick. This has some nice properties like it's impossible to write infinite loops. There's also no "else" statement, which is probably my biggest regret.

> Is Megalo object-oriented natively?

Not really. Teams, players, and (game) objects are first-class citizens, and you can attach a set of "member" variables to each of these. The member variables could be numeric, timers, or references to other objects, teams, or players. There's also a set of global variables. There are no member functions, but there are mechanisms to quickly iterate over objects that match a specific criteria, such as a certain label.

> Who or what group in Bungie made the decision to throw out the tried and trusted gametype setup from previous Halo titles, and why? Was it hard to convince the studio to go for what was definitely a risk?

I did. Megalo started as an experiment/toy just after we shipped Halo 3. It was definitely a risk, but the benefits of iteration and creating new gametypes/fixing bugs post-ship were pretty obvious. At that point we didn't know what the handoff plans with MS were though.

> The previous titles used prebaked gametypes. Were the prebaked gametypes faster and easier to implement, or were the newly scripted gametypes more speedily prototyped, tested, and implemented after the groundwork had been completed?

Megalo was amazing for rapid prototyping and iteration. We developed the gametypes we did without a dedicated multiplayer engineer, which allowed them to spend more time improving the networking code (you can tell, right?). Bugs could be fixed within a playtest session, instead of having to wait until later in the day or the next day for a new binary build of the game. On one occasion someone joked about a character dying & dropping all his stuff looking like a pinata. Derek got out his laptop and wrote a gametype where players dropped a random weapon if they were killed by a melee attack - we were playing it 15 minutes later. On the downside, the final 10% of a game engine like HUD and messaging was a lot harder to manage in Megalo.

> Can any Bungie employee who has the appropriate knowledge script a new gametype, or is the keys to this particular feature reserved for "gametype scripting employees"?

Anyone could write a script, but it would have to go through rigorous testing to ever ship. Only a handful of people are responsible for the scripts you've seen so far.

> How much memory is available for a Megalo scripted gametype? If you can’t answer specifically, would you say it’s “Significant amount” or “Not much”? Is the memory limit dependent on the amount of variable storage or the amount of commands/script or both?

It's not a lot, but it forces you to be clever. Derek was constantly hitting limits in the Invasion script. Sometimes we'd raise the limits, and sometimes he'd just have to make something more efficient.

> From what it seems like, once the engine fires a “Game Over” event, the scripting engine shuts off. Is this what happens, or does a Megalo scripter do this?

Yeah, the script stops updating after "round over."

## Widgets and HUD

> As we’ve seen with the post-ship Race variants, Bungie can add static text (“Number of flips”) and text that represents a changing variable (number of flips). What other widgets are available to scripters?

Text, meters, and icons.

> How much of the default HUD elements can be controlled via Megalo? Can Megalo disable the weapon icon and ammo readout and leave the radar and grenade readouts, or are only a base collection of HUDs (Human, Elite, Monitor, and “blank”) available?

None. It's something we wanted to do originally but didn't pan out.

> Is it possible for Megalo to make a gametype where the HUD graphics are gone but the first person weapon model remains?

Nope.

## Object I/O

> How much inter-object interaction is possible? Is it all collision based? For example, the existing KotH gametype obviously uses “IF player_model IS TOUCHING koth_hill THEN awardpoints”. Can any object interact with any other object via script?

All those interactions are based on the boundary shape set in forge.

> B. For example, you shipped the new label for Invasion called CORE_RESET where if the core is thrown into the boundary of a such labeled object, it gets reset. Could you make a new label that only resets vehicles that enter it’s boundaries?

Probably.

> C. You mentioned the Flag Reset radius is accomplished by creating and attaching a spherical volume to the Flag Object. Can multiple actions be assigned to a single volume? For example, would it potentially be possible for the scripting engine to reset a hog that sits over a flag for more than 15 seconds (flag object can check for a colliding unoccupied hog?

The actions are entirely up to the script. You basically get "is object X inside object Y's bounding volume?" then you can do whatever you want with that information.

> Do certain objects have certain special properties? Example: Rocket Race teleports you if you’re off your vehicle. Is this done by checking to see if the player is in a vehicle (status property) or if the vehicle has occupants (binded objects property)? Can you detect the difference between an occupied and unoccupied vehicle in script?

The script can tell what vehicle a player is in, if any. It's trickier (but not impossible) to tell if a vehicle is occupied or not.

> Can any object be binded to another? For example, in Speedpile the Flag Object is binded to the player biped. Could you clue a bomb to someone’s head, or make it so mongeese in Race have neutral flags on the back of them like go-karts?

You can attach any object to any other. But the parameters for doing so are not really fine-tuned, and some objects don't behave like you might expect when they are attached.

> Since Reach’s multiplayer networking is asynchronous, is there a way for Megalo to sync important variables across all players, or are all internal arrays/labels always just on the host?

Every variable can be marked as networked or local-only. The synching of networked variables is all done automatically behind the scenes. This is one of the huge advantages of Megalo over a hard-coded game engine.

## Object Manipulation
<span name="deviceMachines">
> We know that mid-game object creation is possible (Invasion phase spawning, Race vehicles). Can an object be moved (ie teleport a hog from one location to another) without just deleting it and respawning it?
</span>

The only way to move an object is to attach it to another one (and then optionally detach it).

> Speedpile modifies the size of flags that are worth more points to be bigger. Are only a certain subset of objects able to have their size modified, or can any dynamic object in a .map be modified (giant players, comically big oddball, really big Tunnel, Long piece)

Any object can be scaled but physics models are never scaled (this is a limitation of Havok and also why you can't scale objects in Forge) - so it's not smart to do it on anything other than a certain small set of objects.

> To make up for the lack of an OS effect in Reach, you attached a flame emitter to the biped of players. Are any other emitters available or does this apply to Question 12 (where you just used the ability to attach objects to other objects to achieve this)

I think there is only one object that is designed as an effect emitter for players - the invisible_cube_of_derek.

> Can a player be spawned as a Monitor in any gametype (ex: Chess)? Can the player be able to edit objects in any mode, or is this something that requires the “root” gametype to be Forge-only?

The player never spawns as a monitor (outside forge), but you can force the player to control a different biped (as chess does). Object manipulation is only available in Forge.

## Player Manipulation

> We know various traits (player health/speed/gravity) can be changed during the due to Hill/Zombie/Objective carrier traits. Can affects be applied only per-person, or could you (say) make all of Red Team catch on fire when someone stands inside a Hill Object?

Being on fire is a property of having the invisible_cube_of_derek attached to you.

> The shipping Juggernaut variant forces the Juggernaut’d player to switch to a weapon. Can a player’s weapons be stored in a variable, then forced to a weapon, then forced back to the original weapon? Is it possible for players to be able to choose what weapon the Juggernaut switches to (and toggle his flame effect) or do these HAVE to be scripted only?

There are a few ways to do this. It's not possible to make a new game option that covers all the possible weapons though.

> Is it possible for Megalo to take actions (trait modifcation, kill, teleport) on a player based on weapon they are holding? IE, could you make people that are holding a Sniper Rifle get a waypoint over their head, but it disappears if they drop it?

Yes.

> We’ve seen with the Chess gametype that Megalo can spawn NPC bipeds in a gametype, with predetermined armor configurations. Could a gametype potentially force everyone to a Mark V Spartan with base armor, or does this only apply to special bipeds?

The armor config is only for objects created by the script.

> B. As a followup to 21, the Chess gametype also lets you “take over” a biped by standing in it’s bounding box. Is this true takeover (ie the engine is now saying “you are this biped now”) or is it just done by deleting the biped and respawning the player as the biped?

It is a true takeover.

> C. And finally, if it’s true takeover, would it potentially be possible to use this functionality to do player possession? For example, if you can stand behind an opponent long enough, you can take over their biped, and they can only observe their possessed body walking around, as a crazy silly example.

Possibly. Never tried it - there are probably a lot of weird edge conditions.

> D. Since this functionality also amused me, would it be possible to have a variant of Invasion where an invading Spartan could stand in a hill, drain it down to “capture the disguise”, then they’re switched to an Elite to help them infiltrate the enemy base?

Possibly. He'd probably retain his original team color though.

> Can the scripting engine boot a player out of a game, or just force them to be a spectator?

Megalo has rather limited interaction with the spawning system. The best you could do is delete/kill their biped whenever they spawn.

## Map Manipulation

> The special Invasion: Breakpoint gametype for Breakpoint does neat things like make it so the computer cores raise up while being captured, spawns the special pretty purple Covie bomb for phase 2 (kudos to the artists on that one), and makes the last phase explode with debris when the bomb is armed. Using the default Invasion gametype removes all of these little extra polishes. As a result, Invasion: Breakpoint is locked to that map. Can designers elect to lock a gametype to a map themselves or is this automatically handled by the engine (ie it checks to see if a required object exists on the selected map)?

It's usually done by referencing an object that is only on that map.
> B. Can that Covenant bomb be used in the disc maps or was it a special model made for Breakpoint?

It's only on breakpoint.

> Can you add virtual soft or hardkills to maps via scripts (ie IF PLAYER_X > 500 THEN KILL)? Although I guess this one kind of applies to Meta (accessible variables) and Player Manipulation (player properties)

Not really sure what you're asking. You could destroy/kill any object based on any criteria that Megalo is able to detect.

> Does Megalo have any animation capabilities (ie you could smoothly move a Block 2x4 across Forge World) or are all the custom animations for Spire/Breakpoint/Boneyard just baked .map animations called by Megalo at runtime?

See [here](#deviceMachines). All objects that you see animate in invasion are actually device machines, which Megalo has some limited control over.

## GUI additions
> We’ve seen new toggles such as Supershields added post ship to the custom game GUI. Can Megalo scripters add new submenus?

There is one submenu with script-specific options, that's it.

> We’ve seen with Race that you can add “Number of flips” as a Postgame Carnage Report statistics category. Can you add or remove pages from the PCR with Megalo? For example, could you remove the Kills and Deaths columns in CTF, or add “Time not moving” to a gametype, or something silly like “Amount of time near other players” ?

There is one page in the PGCR dedicated to script-specific stats.

> If you save a gametype from The Arena, you get the dynamic “Rating” readout on the scoreboard. Was this something hard baked into the engine or can Megalo change/add strings to the Scoreboard screen?

The script decides whether or not rating is displayed, but rating is the only thing it can show there.

## Bungie Meta

> If you can find out, besides Slayer, what was the first gametype re-implemented in Megalo?

Warthog soccer (the warthog was the ball) in the little trench on Sandtrap. Starting weapons were rockets and hammers, or you could (try to) drive the warthog across the finish line.

> How much time, from inception -> scripting -> test -> more scripting -> ship does a post ship gametype take to create?

Apart from Invasion or chess, the first 90% of a script could be done in a day or two - but the polishing could take weeks.
