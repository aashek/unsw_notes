## Predicate Logic

### Question 1

For which values of A and B does the boolean expression `φ=¬(A⇒B)∨¬B` hold?

```answer
(a ^ ~b) V ~b
~b V ~b
~b

```



### Question 2

Simplify the boolean expression ``(A⇒B)∨(B⇒A)``

```answer
(~a V b) V (~b V a)
a V ~a V b V ~b
T V T
T
```




```note
~b V b 
=
T 
is not generally ok

it corresponds to a function

constructive logic
```


### Question 3

A binary connective ∙ is defined as follows:

| A   | B   | A ∙ B |
| --- | --- | ----- |
| ⊥   | ⊥ | ⊤   |
| ⊥   |   ⊤  | ⊥      |
| ⊤   |   ⊥  |  ⊤     |
| ⊤    |    ⊤ |  ⊤     |

Restate the formula A∨B in terms of ∙. What is the ∙ connective?

```answer

The ∙ connective is B -> A.
```



### Question 4

Assuming that F(x) states that the person x is my friend and that P(x) states that the person x is perfect, what is a logical translation of the phrase "None of my friends are perfect"?

```answer
All of my friends are not perfect.
Or 
If you are my friend, you are not perfect.

∀x F(x) -> ~ P(x)
```

### Question 5

Given the following function

| f(n) |  |
| ---- | -------------------------- | 
| 0    |   n=0                         |     |
| 2n−1+f(n−1)     |  n>0                          |     |

Prove that ∀n∈N. f(n)=n^2.

```answer

f(0) = 0
= 0^2 

So true for f(0).

Assume true for f(k).
Hypo: f(k) = k^2.

rtp: true for f(k+1)

f(k+1)  = 2(k+1) - 1 + f(k)
		= 2k + 1 + f(k)
		= k^2 + 2k + 1
		= (k+1)^2
```

