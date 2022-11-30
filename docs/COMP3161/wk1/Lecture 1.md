What are types
- abstraction (provides an interface)
- static analysis
	- analyses the logic of the program


Should we have a type system in the first place


? Tut 1 Question ?
Types let you avoid type errors

- How do you know that the type system avoids type errors?

Let us consider the following Java Code

```java
class Shape{}

class Rectangle extends Shape {}

class Triangle extends Shape {}
```

And then lets try to convert a Rectangle to a Triangle.

```java
...

public class Hello {

	public static Trinagle Rectangle2Triangle(Rectangle rect) {
		return ret;
	}
}
```


![[Pasted image 20220913163633.png]]


Two possibilties:
1. The program runs without an error
2. We get some kind of runtime error

Whichever happens we get a violation of a mathematical proerty of type system.
1. subject reduction
   (if i have a well-typed program, that does not do tpye cast, it stays well-typed)
2. progress (the behaviour of every well typed program is well-defined)




Course Content 

We do 3 R's

Read and understand new programming languages
Write your own programming languages
Reason about programming languages in a rigorous way


Read:
- Language researchers create new ones
- Formal verification as proof





![[Pasted image 20220913170120.png]]

