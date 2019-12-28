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