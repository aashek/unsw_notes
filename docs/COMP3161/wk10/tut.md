```toc
```

## Overloading

- Problems with writing custom comparators for multiple classes
- We want to abstract classes so we have a common comparator


Known as typeclasses, or traits in rust, extends class in java.

```haskell

-- there exists a partial ordering on 'a'
class Compare a where
  cmp :: a -> a -> Bool

-- real implementation of compare (extending Compare a)
instance Compare Int where
  cmp x y = x <= y

-- we want to compare a list of elements
instance (Compare a) => Compare [a] where
  cmp xs ys = and (zipWith cmp xs ys)

-- we wish to compare a list of lists
group  :: (Compare a) => [a] -> [[a]]
group []     = []
group (x:xs) = let (ys, zs) = span (cmp x) xs
                in (x:ys) : group zs
```

Haskell will convert the class into a type.
```haskell
type CompareDict a = (a -> a -> Bool)
```

instances get turned into functions or values.

```haskell
instance Compare Int where
  cmp x y = x <= y


intCompDict :: CompareDict Int
intCompDict = (\x y -> x <= y)

-- we want to compare a list of elements
instance (Compare a) => Compare [a] where
  cmp xs ys = and (zipWith cmp xs ys)

 listCmpD :: CompareDict a -> Compare [a]
  cmp xs ys = and (zipWith cmp xs ys)

-- we wish to compare a list of lists
group  :: (Compare a) => [a] -> [[a]]
group []     = []
group (x:xs) = let (ys, zs) = span (cmp x) xs
                in (x:ys) : group zs

```

## SubTyping

### Coercions and Subtyping

You are given the type `Rectangle`, parameterised by its height and width, and the type `Square` parameterised by the length of one of its sides. Neither type is mutable.


a. Which type is the subtype, which type is the supertype?

```
Subtype: Square
SuperType: Rectangle
```

b. Give a subtype/supertype ordering of the following set of function types: `Rectangle -> Rectangle`, `Rectangle -> Square`, `Square -> Rectangle`, `Square -> Square`.

```mermaid
graphBT;
 SqRect --> RectRect;
```

Rect -> Sq ==> Sq -> Rect


Any values in p1 -> p2 must exist in t1 -> t2.

Fix the return type, a

c. Define a data type `Square` and a data type `Rectangle` in Haskell. Then define a coercion function from elements of the subclass to elements of the superclass.

We first decide whether we change the input of the function, or change the output of the function.

```haskell

```


d. Show that the ordering you have given in the previous question is correct by defining coercion functions for each pair of types in a subtyping relationship in part (b).

### Constructor variance

List some examples of a _covariant_, _contravariant_ and _invariant_ type constructor.


## LCR Conditions

Consider the following two processes, each manipulating a shared variable x, which starts out at 0.

**Thread 1**: x:=x+1;x:=x−1;

**Thread 2**: x:=x×2

a) What are the possible final values of x assuming each statement is executed _atomically_?
0, 1.

b) Rewrite the above program into one where each statement obeys the _limited critical reference_ restriction. What are the possible final values now?
-1, 0, 1, 2

c) How could _locks_ be used in your answer to (b) to ensure that only the final results from part (a) are possible?

var t;
take(l);
t := x;
x := t + 1;
release(l);
take(l);
t := x;
x := t - 1;
release(l);

var u;
take(l);
u :=x;
x:= u * 2;
release(l);




After p2, wantp is set to 1 or -1, or abs val is 1.
After q2, wantq is set to 1 or -1, or abs bal is 1.

in other for both critical sectios to be passed, we must have both await clauses to be true.
wantp != wantq, and wantp != -wantq.



if both are set to 1 it could run both,

we run p2 and q2 at the same time,
however we assign only one of them
i.e.
wantq = -1.
then run q3, and pass into the critical section infinitely.

then we assign p2.
wantp = 1
we check the statement wantp != wantq (1 != -1) which passes into the critical section.


