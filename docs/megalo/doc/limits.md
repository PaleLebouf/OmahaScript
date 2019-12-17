<style type='text/css'>
ul.nav {list-style-type: none;padding: 0;overflow: hidden;background-color: #333;}
li.nav {  display:block; float: left;}
li.nav a {display: block; color: white; text-align: center; padding: 14px 16px; text-decoration: none;}
li.nav a:hover:not(.active) {background-color: #111;}
li.nav a.active {background-color: #ffcc00; color:#000} </style>
<ul class="nav">
      <li class="nav"><a href="https://palelebouf.github.io/OmahaScript/">Home</a></li>
      <li class="nav"><a class="active" href="https://palelebouf.github.io/OmahaScript/megalo/doc/home">Megalo Documentation</a></li>
      <li class="nav"><a href="https://palelebouf.github.io/OmahaScript/megalo/qna">Megalo QnA</a></li>
</ul>

# Limits 

Megalo itself has a lot of limitations in what it can and can't do, as outlined in [the QnA](https://palelebouf.github.io/OmahaScript/megalo/qna).

It's a great and dynamic tool for creating something as complex as chess, spawning usually unspawnable objects on certain maps pre MCC (campaign falcons, forklifts, fire, and more) but it can't perform things such as custom animations that aren't already part of the map like moving ships in invasion.

Technical limitations are very restrictive, considering that most gametype logic needs to be networked between host and client, so the amount of variables that you can "create" or use in megalo is also very limited.

## General Limitations

These are the overarching limitations placed upon Megalo and Megalo Script.

|        Property        	| Number Limit 	| Description                                                                                                                                                                  	|
|:----------------------:	|:------------:	|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| Maximum Trigger Groups 	|      128     	| This is the maximum number of triggers that can be defined and utilized in the scripting section of megalo. This includes iterating functions on each player or game object. 	|
| Maximum Script Values  	| 4096         	| The maximum number of gametype-specific values, showing up in menus as well as in-game networked variables.                                                                  	|

## Scripting Specific Limitations

### Entry Points

Entry points are like a predefined point to start at certain main stages of a match. There are 7 entry points:

1. Initialization - Think of this like a constructor function for a gamemode, specifically for the host I believe.
2. LocalInitialization - This is a constructor for the gamemode but for the other players in the lobby.
3. HostMigration - Self explanatory, this entry point runs when there's a single host migration.
4. DoubleHostMigration - Same as HostMigration but when it happens twice in a row.
5. ObjectDeathEvent - Ran when an object is deleted, like when the oddball is thrown into a kill barrier and it's deleted. 
6. Local - Ran locally for everyone.
7. Pregame - Self explanatory. This is when the announcer says what gametype it is, displays the gametype and description, and the final countdown before game start occurs.


