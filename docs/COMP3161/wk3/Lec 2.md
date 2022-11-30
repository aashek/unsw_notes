Semantics are made up from dynamic and static elements.

Dynamic Semantics
- what programs actually do


#### Dynamic
Behaviour
- Final Result
Cost
- Resources
- Time
- Space

Static semantics
aspects of P that can be determined without running the program

e.g.
```haskell
Arith ::= Num Nat
		| Var String
		| Plus Arith Arith
		| Times Arith Arith
		| Let String Arith Arith



```

We can check from static semantic if the program is well-scoped.



Gamma is context.

ok is a binary judgement on context and terms.



Unprovable because its an empty set and we want to find x bound.

We started from empty context.
y bound == example  y is a global variable and cannt be used or "bound".
.


