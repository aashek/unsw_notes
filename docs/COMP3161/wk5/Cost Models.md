A cost model is a mathematical model that measures the cost of executing a program.

```toc
```


-- how to evaluate the cost of a machine

## Operation Cost Model
Time cost is determined by counting the number of steps it takes to finish.


## Abstract Machine (M Machine)
An abstract machine consists of:
A set of states $\sum$ 
A set of initial states $I \subseteq \sum$
A set of final states $F \subseteq \sum$
A transition relation $\mapsto \subseteq \sum \times \sum$
(small step definition)

`small explanation`
`e1 evals to e1'`
`so machine wise, they are the same`

```
v is a function
left side is also a function
apply recfun f.x.e. v
for all x, replace with v
bu
```


![[Pasted image 20221101084714.png]]

-- however there are issues with applying this idea to small step 

We expect a machine to perform small step in O(1) time.
However this is not the case for evaling.

Two problems:
- Substitution occurs in function application, which is potentially O(n) time (we dont know what 1 step leads to)
- Control Flow is not explicit - (do we know that the recursive step oneStep e_1 evals to Num n?)

```
eval (Num n) = n
eval e       = eval (oneStep e)  [We dont know if substitution is O(1)]

oneStep (Plus (Num n) (Num m)) = Num (n + m)
oneStep (Plus (Num n) e_2)     = Plus (Num n) (oneStep e_2)
oneStep (Plus e_1 e_2)         = Plus (oneStep e_1) e_2


```

-- substitution is potentially O(n)



## The C Machine

We define a machine where all the rules are axioms, without recursive definitions.

This is typically implemented into a stack, where at every small step, we consider the stack and expression.

Frames |> Stack

![[Pasted image 20221101085942.png]]
Unsolvable expressions are normally called frames.
---- (Plus 3 "") where "" is being evaluated 
- Explicit information that is evaluated are put on the 'stack' 
--- (Frames) |> eval Num 3

![[Pasted image 20221101090239.png]]

### Evaluating in C machine

Now if we evaluate, we use the rules below.

![[Pasted image 20221101090258.png]]


### Example: Plus (Plus 2 3) 4)

Take for example Plus e_1 e_2

In English we want to evaluate in the order:
Plus e_1 e_2
-> Plus (eval e_1) e_2
-> Plus v1 e_2
-> Plus v1 (eval e_2)
-> Plus v1 v2
-> v1 + v2

In the stack we want to store (current) unsolvable exprs as frames.

![[Pasted image 20221101090308.png]]


## Other Rules
Here are the rest of the rules
![[Pasted image 20221101091123.png]]
![[Pasted image 20221101091129.png]]


## Definition of C Machine 
Control Flow Machine
All rules are axioms
- the evaluator can run until the stack is solved
We have a lower-level specification
Substitution is still a machine operation
- still not O(1) per step since substitution is not O(1)


## Comparison C vs M machines

C machines are more detailed than M machines, but they both produce the same result.
This is called explicit stacks

## How to Prove Refinement
We have assumed that the C machine works the same as the M machine, but how do we prove it?

## Abstraction Function

![[Pasted image 20221101091600.png]]

This is essentially pattern matching from C machine to M machine.


We define three simple rules, which can be applied inductively
![[Pasted image 20221101092221.png]]



### Case 1 : Plus e_1 e_2
![[Pasted image 20221101092250.png]]

### Case 2 : Plus _ e2
![[Pasted image 20221101092844.png]]

### Case 3 : Plus e1 _

![[Pasted image 20221101092916.png]]