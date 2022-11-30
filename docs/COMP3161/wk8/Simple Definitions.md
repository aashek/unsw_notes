```toc
```


## Atomic Elements
We run the entire program without any interjections/stopping
```haskell
Thread 1 : x:= x + 1; x:= x - 1;
Thread 2 : x:= x ** 2;
```

## Limited Critical Reference
Any line of code access a variables two times, we don't know which occurs first.



## Functional Programming Language
In essence, a programming language which allows lambda.
Examples: Haskell, JavaScript, (Lisp?)


## Quaternary Judgement
`_ ; _ ⊢ _ ok ⇝ _`

## Free Variable

A variable that is declared, that can be written to.

## Initialized Variable
A variable that has been declared, and has a value.
```c
var y ⬝
// here, y is declared (free)
var x ⬝
// here, y,x are declared (free)
y := 0;
// here, y is declared and initialised, x is declared
x := y + 1
// here, x,y are declared and initialised
```
