<style type='text/css'>
ul.nav {list-style-type: none;padding: 0;overflow: hidden;background-color: #333;}
li.nav {  display:block; float: left;}
li.nav a {display: block; color: white; text-align: center; padding: 14px 16px; text-decoration: none;}
li.nav a:hover:not(.active) {background-color: #111;}
.active {background-color: #ffcc00;} </style>
<ul class="nav">
      <li class="nav"><a href="https://palelebouf.github.io/OmahaScript/">Home</a></li>
      <li class="nav"><a class="active" href="https://palelebouf.github.io/OmahaScript/megalo/doc/home">Megalo Documentation</a></li>
      <li class="nav"><a href="https://palelebouf.github.io/OmahaScript/megalo/qna">Megalo QnA</a></li>
</ul>
# Conditions

Conditions are one of the greatest tools in the toolbox for making custom game modes. These are how you'll
determine what's going on in game to adjust things accordingly. 

### Comparison Operators
To start off, there's a basic set of operators that should be familiar to any programmer. These are the only ones that
are available. In the table below, the TypeID is how Megalo figures out which operator to use. This TypeID is also how they appear in
decompiled Megalo XML files:

| TypeID 	| Operator 	|
|:------:	|:--------:	|
|    0   	|   < (Less Than)    	    |
|    1   	|   > (Greater Than)        |
|    2   	|   == (Equal)    	    |
|    3   	|  <= (Less Than Equal)     |
|    4   	| >= (Greater Than Equal)   |
|    5   	|    != (Not Equal)         |
