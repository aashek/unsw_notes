
Red Black Tree 
```haskell
data RBColour
  = Red
  | Black

data RBTree
  = RBLeaf
  | RBNode RBColour Item RBTree RBTree
```

Red and Black are RBColours.
$$
\frac{}{Red\ RBColour}\;\frac{}{Black\ RBColour}
$$
An RBLeaf is a type of RBTree.
$$
\frac{}{RBLeaf\ RBTree}
$$

A tree can be created from a colour c, an item x, and two RBTrees, t1 and t2.
$$
\frac{c\ RBColour\ \ x\ Item\  \ t_1\ RBTree\ \ t_2\  RBTree}{RBNode\ c\ \ x \ \ t_1\ \ t_2\ \ RBTree}A_L
$$

In real life, RBTrees are the following cases
- Black nodes can have black children
- Red nodes cannot have immediate red children

Red Root, Black t1, Black t2


We define a subclass OK_R to demonstrate that an OK tree is a tree with a red node.

We note the following about our class

OK_R t1 OK_R t2 => Black OK
OK t1 OK t2 => Red OK_R
OK => OK_R (can change OK to OK_R)

This satisfies the following
- Black trees can be created from two black nodes
- Black tress can be createdf rom two red nodes
- Black trees...
- Red trees can be created only by 2 black nodes (i.e. OK_R cannot be used to construct an OK_R tree)