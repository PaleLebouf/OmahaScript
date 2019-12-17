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

|        Property        	| Number Limit 	| Description                                                                                                                                                                  	|
|:----------------------:	|:------------:	|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| Maximum Trigger Groups 	|      128     	| This is the maximum number of triggers that can be defined and utilized in the scripting section of megalo. This includes iterating functions on each player or game object. 	|
| Maximum Script Values  	| 4096         	| The maximum number of gametype-specific values, showing up in menus as well as in-game networked variables.                                                                  	|
