<style type='text/css'>
ul {list-style-type: none;padding: 0;overflow: hidden;background-color: #333;}
li {  display:block; float: left;}
li a {display: block; color: white; text-align: center; padding: 14px 16px; text-decoration: none;}
li a:hover:not(.active) {background-color: #111;}
.active {background-color: #ffcc00;} </style>
<ul>
      <li><a class="active" href="https://palelebouf.github.io/OmahaScript/">Home</a></li>
      <li><a href="https://palelebouf.github.io/OmahaScript/megalo/doc/home">Megalo Documentation</a></li>
      <li><a href="https://palelebouf.github.io/OmahaScript/megalo/qna">Megalo QnA</a></li>
</ul>
# Conditions

This is one of the greatest tools in the toolbox for making custom game modes. These are how you'll
keep track of what's going on in game and adjust things accordingly. To start off, there's a basic set
of operators that should be familiar to any programmer. These are the only ones that are available.
In the table below, the TypeID is how Megalo figures out which operator to use. This TypeID is also how they appear in
decompiled Megalo XML files:

### Comparison Operators
| TypeID | Operator |
| ------ |:---------------------: |
|   0  | < (Less Than) |
|   1  | > (Greater Than) |
|   2  | == (Equal) |
|   3  | <= (Less Than Equal) |
|   4  | >= (Greater Than Equal) | 
|   5  | != (Not Equal) | 

| TypeID 	| Operator 	|
|:------:	|:--------:	|
|    0   	|     <    	|
|    1   	|     >    	|
|    2   	|    ==    	|
|    3   	|    <=    	|
|    4   	|    >=    	|
|    5   	|    !=    	|
