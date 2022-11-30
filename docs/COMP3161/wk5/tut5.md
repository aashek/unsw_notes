```toc
```


1. 
	1. Most imperative programming languages do not make the else clause of an if statement mandatory. TinyImp only has the if then else form. How can a stand-alone if be encoded in TinyImp?
	2. Conversely, how can if then else be encoded using only stand-alone if-   in TinyImp?
	3. MinHS doesn't have stand-alone if, a design decision shared by most functional programming languages. Unlike TinyImp, there's no sensible way of encoding it. Why is it difficult to encode, and why do you think the language has been designed this way?

[[TinyImp#TinyImp Definition]]


1.1.
```
if b then e fi === if b then e else skip fi
```

1.2.
(we want to create if then else with an unknown guard)
In the following, we assume x is a fresh variable, i.e.,one that doesn't occur free anywhere in e1, e2 or b. To see why we bother with x, consider what happens if the truth value of b changes as a result of executing e1.
```
if b then e fi 
===

varx⋅
x:=b;
if x then
 e1
fi;

if ¬x then
 e2 
fi
```


1.3.
The if in TinyImp is a statement and therefore has no value, only side-effects. Hence there's a clear choice of what to do when the guard is false: nothing. In MinHS, if then else is an expression, and wea would like expressions to have values. In the absence of an else

branch, it's not clear what value we should assign to an expression whose guard is false.

If we really want to go ahead with this, we might consider the following choices. First, we could say that if

expressions whose guard are false have no value, and cause the program to diverge or abort. Second, we could associate a "default" value to every type, and use this value as a fallback. There's nothing inherently wrong with either choice, but both seem to run against the programmer's intution that nothing should happen.



## Abstract Machines

![[Pasted image 20221104152932.png]]

We label the stack as P

Rule 1
If we are evaling P on the stack, then we return P.
if s $\prec$ P $\mapsto$ s$\succ$ P

if we are evaling a+b, we want to eval the left side first
so we place a box in the place of the a.

If we are have p + box as a frame, and have a value A on the stack, we can remove the frame and return P + A == AP.



![[Pasted image 20221104153341.png]]