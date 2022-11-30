## Parsing Relation

Using the inference rules for the parsing relation of arithmetic expressions given in [the syntax slides](https://www.cse.unsw.edu.au/~cs3161/22T3/Week%2002/Thursday/Slides.pdf), derive the _abstract syntax_ corresponding to the _concrete syntax_ 
`3 + let x = 5 in x + 2 end`.

(Num 3) Plus (x )


## Substitution

What is the result of the substitution in the following expressions?

1.  (Let x (y. (Plus (Num 1) x)))[x:=y]
(Plus (Num 1) x) = x + 1


-   (Let y (z. (Plus (Num 1) z))[x:=y]

-   (Let x (z. (Plus x z))[x:=y]

-   (Let x (x. (Plus (Num 1) x))[x:=y]

## Semantics

You may want to look at the W3 Thursday notes before attempting these questions.

A robot moves along a grid according to a simple program.

The program consists of a sequence of commands `move` and `turn`, separated by semicolons, with the command sequence terminated by the keyword `stop`:

R::=move; R | turn; R | stop

Initially, the robot faces east and starts at the grid coordinates `(0,0)`. The command `turn` causes the robot to turn 90 degrees counter-clockwise, and `move` to move one unit in the direction it is facing.

### Denotational Semantics

First, devise a suitable _denotational semantics_ for this language. For this exercise, we are only interested in the final position of the robot, so the mathematical object which we associate to the sequence of instructions should merely be the final coordinates of the robot as a 2D vector.

[[⋅]]:R→Z2

### Operational Semantics

#### Small-Step Semantics

Next, we will devise a set of small-step semantics rules for this language.

This means determining answers to the following questions:

1.  What is the set of states?
2.  Which of those states are final states, and which are initial states?
3.  What transitions exist between those states?

#### Big-Step Semantics

Lastly, we will devise a set of big-step evaluation rules for this language.

This means determining answers to the following questions:

1.  What is the set of evaluable expressions?
2.  What is the set of values?
3.  How do evaluable expressions evaluate to those values?

## Lambda calculus and binding

### Reduction

Apply β

and η reduction as much as possible to this term, until you reach a _normal form_. Where necessary, use α

renaming to avoid capture.

(λn f x. f (n x x)) (λf x. f)

### de Bruijn Indices

How would the above λ

term be represented in de Bruijn indices? Repeat the same reduction with de Bruijn indices.