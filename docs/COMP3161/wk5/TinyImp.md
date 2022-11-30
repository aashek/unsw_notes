
```toc
```

## TinyImp Definition

We define TinyImp as a language based on structural programming.
The syntax consists of statements and expressions.

```c
Stmt ::= skip                                     Do nothing  
| x := Expr                                       Assignment  
| var y · Stmt                                    Declaration  
| if Expr then Stmt else Stmt fi                  Conditional  
| while Expr do Stmt od                           Loop  
| Stmt ; Stmt                                     Sequencing

Expr ::= 〈Arithmetic expressions〉
```

Some example functions can be written in this format.

```c
// Factorial
var i ·  
var m ·  
i := 0;  
m := 1;  
while i < N do  
	i := i + 1;  
	m := m × i  
od
```

```c
// Fibonacci
var m · var n · var i ·  
m := 1; n := 1;  
i := 1;  
while i < N do  
	var t · t := m;  
	m := n;  
	n := m + t;  
	i := i + 1  
od
```


## Checking Syntax in TinyImp

Variables need to be checked in this syntax, since we can write valid syntax, but fails to run.
```c
var m 
m := n + 1; // n is not declared
```

[[Simple Definitions#Free Variable]]
[[Simple Definitions#Initialized Variable]]
![[Pasted image 20221030111050.png]]
In essence:
- U is the declared variables
- V is the initialized variables (have a current value)
- W is which variables are newly initialized from running (definitely written to)

So now we create some checking rules for variables using U V and W.

### Skip

![[Pasted image 20221030113653.png]]
In the skip program, skip is ok, then no unsafe writes happens.
W is the definitely written variables (where nothing was written to)

### Assignment

`x := Expr`
We assume the statement x:=e is ok, giving us W.
We need to check that x is free and not initialized, or we overwrite a value.
We need to check that inside the expression e, we are not using undeclared variable (runtime error), so we check all free variables in e are declared.
This gives us x inside of W, since we changed x.
![[Pasted image 20221030114344.png]]

### Variables

If y is free, then we can initialize var y.
But what if the statement s uses the variable.
if s initializes y, then we dont keep the value in the outer function.

![[Pasted image 20221030114446.png]]


### If then else

We need the guard to have declared variables. FV(e)
statement 1 definitely defines W_1.
statement 2 definitely defines W_2.
W is the definitely declared variables of both statements. Hence its the variables that exist in W_1 and W_2. Or the intersection of both sets.


![[Pasted image 20221030141200.png]]


### While

The definitely declared variables is zero. This is because the loop can run zero times.
We need to know that the variables we are using are written to already.
We just define, but dont use the definitely declared variables in the do statement.

![[Pasted image 20221030141858.png]]


When we run s1, we know the variables definitively set are W_1. Then we run statement 2, using the context of the previous statement.
Hence s1 produces W_1, and s2 must use them as declared variables.
And the final result depends on both statements definitely defined variables.

![[Pasted image 20221030142058.png]]


# Dynamic Semantics

We will use big-step operational semantics. What are the sets of  
evaluable expressions and values here?  
**Evaluable Expressions:** A pair containing a statement to execute  
and a state σ.  
**Values:** The final state that results from executing the statement.  
**States:** mutable mappings from states to values.

![[Pasted image 20221030155332.png]]

![[Pasted image 20221030155341.png]]

For every loop interaction we apply the bottom right rule n times.


## Uninitialized Variables

We can evaluate this behaviour in the big step semantics, and prove its impossible.

![[Pasted image 20221030163003.png]]

But what if we wanted to define actual behaviour for this (make it valid compile and run)

### Crash and Burn
Using an uninitialized variable is undefined, and does not 'reduce' to a value.
![[Pasted image 20221030170425.png]]



### Default Value
Using Java, declarations of variables have a default value of 0.
So whenever we declare a variable, we set it to 0.
![[Pasted image 20221030170311.png]]

### Junk Data
Using C, we can allocate memory but we havent cleared the value yet.
- When declaring x, We get a random value n (default value is not zero)
![[Pasted image 20221030170323.png]]