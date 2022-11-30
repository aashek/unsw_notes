## Inductive Types

Consider the `(++)` operator in Haskell.

```haskell
(++) :: [a] -> [a] -> [a]
[]     ++ ys = ys
(x:xs) ++ ys = x : (xs ++ ys)
```

1.  State the formal properties of _left identity_, _right identity_ and _associativity_ for `(++)`. For information look at [[Identity Laws]].
2.  Try to prove these properties. In some cases, you may need to perform induction on the structure of lists. The **base case** of the induction will be for the empty list, and the **inductive case** will be to show your property for a list `(x:xs)`, assuming the property for the list `xs` (this assumption is called the _inductive hypothesis_).

```answer
1. 
Left identity
x ++ [] = x
Right identity
[] ++ x = x
Associativity
(x ++ y) ++ z = x ++ (y ++ z)

2.
Left
xs ++ [] == xs
trivial by definition

Right 
[] ++ xs == xs
Base x = []
LHS : [] ++ [] 
	= [] {By 1st definition of (++)}

IH : [] ++ ys == ys

RTP: [] ++ x:ys == x:ys
LHS: [] ++ x:ys
	= x:ys {By 1st definition of (++)}
	= RHIS



Assoc
(x ++ y) ++ z == x ++ (y ++ z)
Base:
([] ++ y) ++ z == [] ++ (y ++ z)
LHS: ([] ++ y) ++ z
	= y ++ z {By 1st definition of (++)}
RHS: [] ++ (y ++ z)
	= y ++ z {By 1st definition of (++)}
	= LHS

IH: (xs ++ y) ++ z == xs ++ (y ++ z)

RTP: (x:xs ++ y) ++ z == x:xs ++ (y ++ z)

LHS: (x:xs ++ y) ++ z
	= x:(xs ++ y) ++ z {By 2nd definition of (++)}
	= x:(xs ++ y ++ z) {By 2nd definition of (++)}
	
RHS: x:xs ++ (y ++ z)
	= x:(xs ++ y ++ z) {By 2nd definition of (++)}
	= LHS
```



## Red Black Trees

Red-black trees are binary search trees where each node in the tree is coloured either red or black. In C, red-black trees could, for example, be encoded with the following user-defined data type:

```c
typedef struct redBlackNode* link;

struct redBlackNode { 
  Item item; // Item type defined elsewhere
  link left, right; 
  int  isRed; // 1 if node is red, 0 if black
};

```

and in Haskell (again, we assume the `Item` type is defined elsewhere)

```haskell
data RBColour
  = Red
  | Black

data RBTree
  = RBLeaf
  | RBNode RBColour Item RBTree RBTree 
```

1.  The user defined Haskell data type characterises a set of terms as `RBTree`. List the inference rules to define the same set. Assume there already exists a judgement x Item which is derivable for all x-   in the `Item` type.
2. In a proper red-black tree, we can never have a red parent node with a red child, although it is possible to have black nodes with black children. Moreover, the root node cannot be red. Therefore, not all terms of type `RBTree` are real red-black trees. Define inference rules for a property t OK, such that OK is derivable if the term t represents a proper red-black tree.

$$
\frac{}{Red\ RBColour}A_RBC\;\frac{}{Black\ RBColour}A_RBC
$$
$$
\frac{}{RBLeaf\ RBTree}A_L
$$
$$
\frac{c\ RBColour\ \ x\ Item\  \ t_1\ RBTree\ \ t_2\  RBTree}{RBNode\ c\ \ x \ \ t_1\ \ t_2\ \ RBTree}A_L
$$

2.
$$
\frac{x\ Item\  \ t_1\ OK^R\ \ t_2\  OK^R}{RBNode\ Black\ \ x \ \ t_1\ \ t_2\ \ OK}A_{OK_B}
$$


## Ambiguity and Syntax

Consider the language of _boolean expressions_ (with operators: ∧ (and), ∨ (or), ¬ (not), constant values True and False, and parentheses).

1.  Give a simple (non-simultaneous) inductive definition for this language using only judgements of the form e Bool.

2. Identify how this language is _ambiguous_: That is, find an expression that can be parsed in multiple ways.
3. Now, give a second definition for the same language which is not ambiguous. (to disambiguate: ¬ has the highest precedence; ∧ has a higher precedence than ∨-   , both are left associative).
4. Assume you want to prove a property P for all boolean expressions using rule induction over the rules of the first version. Which cases do you have to consider? What is the induction hypothesis for each case?

<hr>
1.
$$
\frac{}{T\ Bool}\;\frac{}{F\ Bool}\;
\frac{e_1\ Bool\ \ e_2\ Bool}{e_1\ ∧ \ e_2 \ Bool}\;
\frac{e_1\ Bool\ \ e_2\ Bool}{e_1\ ∨ \ e_2 \ Bool}\;
$$
$$
\frac{e_1\ Bool}{~e_1\ Bool}\;
\frac{e_1\ Bool}{(e_1)\ Bool}\;
$$

2. This definition is ambiguous, take for example T V T V T.
$$
\dfrac{\dfrac{\dfrac{}{T\ Bool}\;\dfrac{}{T\ Bool}\ \ \ \;}{{T\ ∨ \ T \ Bool}\;}\dfrac{}{T\ Bool}}{T\ ∨ \ T\ ∨ \ T \ Bool} + \text{mirror image}
$$

3.
exp -> Aexp
Aexp -> Oexp
Aexp & Oexp = e1 ^ e2 Aexp
Oexp ^ Aexp = e1 V e2 Oexp



## Simultaneous Induction

In the lecture, we discussed two alternative definitions of a language of parenthesised expressions:
![[Pasted image 20220915213530.png]]
In the lecture, we showed that if s M, then s L. Show that the reverse direction of the implication is also true, and therefore M defines the same language as L.
_Hint_: similar to the proof discussed in the lecture, it is not possible to prove it using straight forward rule induction. However, first try induction and to see what is missing, then adjust your proof accordingly.

prove a lemma 
to prove the proof

assume sn or sl then sm
