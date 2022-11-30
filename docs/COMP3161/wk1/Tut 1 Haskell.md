## Haskell lexical structure

1.  What is the difference between a `data` and a `type` declaration?

Data is an enumerated list of types, where you can include algebraic data types.
A type is a declaration of kind. 'String', "Char", "Int"

```haskell
data List a =  Nil | Cons a (List a)
type IntList = List Int
```

3.  What is the difference between a _type_ and a _data constructor_? List the identifiers in the code which represent _type names_, and those which represent data _constructor names_.


5.  Which phase of the compiler would be responsible for distinguishing type and data constructors?


## Haskell programming
1.  Write a Haskell function `mySum` that sums all elements in a list of numbers. Feel free to use the following template:
    
    ```haskell
    mySum :: [Int] -> Int
    mySum []     = ???
    mySum (n:ns) = ???
    ```

```haskell
mySum :: [Int] -> Int
mySum []     = 0
mySum (n:ns) = n + mySum ns
```

2.  Write a Haskell function `myProduct` that multiplies all elements in a list of numbers.

```haskell
myProduct :: [Int] -> Int
myProduct []     = 1
myProduct (n:ns) = n * mySum ns

myProduct2 :: [Int] -> Int
myProduct2 []     = 0
myProduct2 [x]     = x
myProduct2 (n:ns) = n * mySum ns

myProduct3 :: [Int] -> Int
myProduct2 xs = foldr (*) 1 xs

```

3.  You probably used copypaste to solve the previous question, didn't you? No reason to be ashamed, we've all done it! But let's try not to.
    
    Find a generalisation `myBinop` that applies a given binary operator `f` with unit element `z` to a list of numbers. We will then be able to define `myProduct` and `mySum` using `myBinop`.


	```haskell
	myBinop :: (Int -> Int -> Int) -> Int -> ([Int] -> Int)
    myBinop f z [] = ???
    myBinop f z (n:ns) = ???
    
    mySum :: [Int] -> Int
    mySum ns = myBinop (+) 0 ns
    
    myProduct :: [Int] -> Int
    myProduct ns = myProduct (*) 1 ns
    ```

```haskell
myBinop :: (Int -> Int -> Int) -> Int -> ([Int] -> Int)
myBinop f z [] = z
myBinop f z (n:ns) = myBinop f (f z n) (ns)

myBinop2 = foldr

mySum :: [Int] -> Int
mySum ns = myBinop (+) 0 ns

myProduct :: [Int] -> Int
myProduct ns = myBinop (*) 1 ns
```


4.  We just reinvented a wheel. The [fold functions](https://hackage.haskell.org/package/base-4.17.0.0/docs/Data-List.html#g:3) are general-purpose library functions that completely subsume `myBinop`. Try to implement `mySum` and `myProduct` using `foldr` instead of `myBinop`.
    
    The linked library documentation references a lot of concepts that we don't assume familiarity with, so don't worry if you don't fully understand it. Perhaps start by looking at the examples.
    
```haskell
mySum :: [Int] -> Int
mySum ns = foldr (+) 0 ns

myProduct :: [Int] -> Int
myProduct [] = 0
myProduct ns = foldr (*) 1 ns
```


## Subtyping Sins

The Monday lecture [[Lecture 1]] demonstrated a flaw in Java's static type system. It's been there for decades and it's well-known, including by the Java developers. Yet they've chosen not to fix it. Why do you think that is?

