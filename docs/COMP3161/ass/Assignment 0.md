# Part A (25 marks)

Consider the language of boolean expressions $\mathcal{P}$ containing just literals (True, False), parentheses, conjunction (∧) and negation (¬):  
`P = {True, False, ¬True, ¬False, True ∧ False, ¬(True ∧ False), . . . }`
1. *Write down a set of inference rules that define the set $\mathcal{P}$. The rules may be ambiguous. (5 marks)*
$$
\begin{gather}
\dfrac{}{True\ Expr}\\\\
\dfrac{}{False\ Expr}\\\\
\dfrac{e\ Expr}{\negate e\ Expr}\\\\
\dfrac{e\ Expr}{(e)\ Expr}\\\\
\frac{e_1\ Expr\ \ e_2\ Expr}{e_1\ ∧ \ e_2 \ Expr}\;
\end{gather}
$$

<hr>
2. *The operator ¬ has the highest precedence, and conjunction is right-associative. Define a set of simultaneous judgements to define the language without any ambiguity. (5 marks)*

We define AExpr, and BExpr, where BExpr has lower precedence than AExpr.
$$
\dfrac{e\ AExpr}{e\ BExpr}\;
$$
True and False have equal highest precedence.
$$
\dfrac{}{True\ AExpr}\;
\dfrac{}{False\ AExpr}\;
$$
Negation has the highest precedence.
By using parentheses, we increase predecence.
$$
\dfrac{e\ AExpr}{¬e\ AExpr}\;\ \dfrac{e\ BExpr}{(e)\ AExpr}
$$
Conjuctions have less precedence then A, hence if we combine an A and a B, we get a B.
Right associative means we need the right element to be a BExpr.
$$
\frac{e_1\ AExpr\ \ e_2\ BExpr}{e_1\ ∧ \ e_2 \ BExpr}\;
$$
<hr>
3. Here is an abstract syntax B for the same language:  
`B ::= Not B | And B B | True | False`  
Write an inductive definition for the parsing relation connecting your unambiguous  judgements to this abstract syntax. (5 marks)  

$$
Abstract\ Syntax
$$
$$
\dfrac{i\in \{True, False\}}{(Bool\ i) \ AST}
\dfrac{a\ AST}{(Not\ a)\ AST}
\dfrac{a\ AST\ \ b\ AST}{(And\ a\ b)\ AST}
$$

$$
\text{Parsing Relation}

$$
$$
\dfrac{i\in \{True, False\}}{i\ AExpr
\longleftrightarrow(Bool\ i) \ AST}
$$

$$
\frac{
e_1\ AExpr\longleftrightarrow\ e_1' \ AST
\quad\quad
e_2\ BExpr\longleftrightarrow\ e_2' \ AST
}{
e_1\ ∧ \ e_2 \ BExpr
\longleftrightarrow\ (And\  \ e_1'\ e_2') \ AST
}\;
$$
$$
\dfrac{e\ AExpr\longleftrightarrow\ e' \ AST}
{¬e\ AExpr\longleftrightarrow\ (Not \ e') \ AST}
\;\ 
\dfrac{e\ BExpr\longleftrightarrow\ e' \ AST}
{(e)\ AExpr
\longleftrightarrow
\ e' \ AST
}
$$
$$
\dfrac{e\ AExpr\longleftrightarrow\ e' \ AST}
{e\ BExpr
\longleftrightarrow
\ e' \ AST
}
$$

<hr>
4.
Here is a big-step semantics for the language
$$\begin{gather}
&\dfrac{ \quad }{ \mathsf{True} \Downarrow \mathsf{True} }(B_1)\quad
&\dfrac{ \quad }{ \mathsf{False} \Downarrow \mathsf{False} }(B_2)\\\\
&\dfrac{ x \Downarrow \mathsf{True} }{\mathsf{Not}\ x\Downarrow\mathsf{False}}(B_3)\quad
&\dfrac{ x \Downarrow \mathsf{False } }{\mathsf{Not}\ x\Downarrow \mathsf{True}}(B_4)\\\\
&\dfrac{ x \Downarrow \mathsf{False } }{\mathsf{And}\ x\ y \Downarrow \mathsf{False}}(B_5)\quad
&\dfrac{ x \Downarrow \mathsf{True} \quad y \Downarrow v }{\mathsf{And}\ x\ y \Downarrow v}(B_6)
\end{gather}
$$

a) Show the evaluation of And (Not (And True False)) True with a derivation tree. (5 marks).

$$
\dfrac
{\dfrac
{\dfrac
{\dfrac{}{True\ ⇓\ True\;}(B_5)\ \dfrac{}{False\ ⇓\ False\;}(B_6)}
{(And\ \ True\ False)\ ⇓\ False}(B_4)
}
{(Not\ \ (And\ \ True\ False))\ ⇓\ True}(B_2)
\;\dfrac{}{True\ ⇓\ True\;}(B_5)
}
{And\ \ (Not\ \ (And\ \ True\ False))\ \ True\ ⇓\ True}(B_4)
$$
<hr>
b) Consider the following inference rule:  
$$\dfrac{y ⇓ False}  
{And\ x\ y ⇓ False}
$$
If we assume that x B holds, is this rule derivable? Is it admissible? And if we don’t assume that x B holds, how does this change your answers? Justify your answers. (5 marks)

$$\text{Assuming x B}
$$
The inference rule R cannot be derived. This is because there is no way to construct a tree that looks like:
$$\dfrac{
	\dfrac{y ⇓ False}
		{\vdots
		}
}{And\ x\ y ⇓ False}\;
$$
However this rule is admissible, since it does not add strings to B. In this case if the result is used in the other inference rules, since x holds in B and y holds in B, that result will also hold in B.

$$\text{Not Assuming x B}
$$
The inference rule R cannot be derived. This is because there is no way to construct a tree that looks like:
$$\dfrac{
	\dfrac{y ⇓ False}
		{\vdots
		}
}{And\ x\ y ⇓ False}\;
$$
This rule is not admissible with the current assumption, since it adds strings to B. This is because x does not hold in B, and if we use x in the other rules, we will get something is also not admissible in B.

<hr>
<hr>
# <hr><hr>

# Part B (20 marks)  
Here is a small-step semantics for a language L with True, False and if expressions:  
L:: True | False | If L then L else L
$$
\begin{gather}
    \dfrac{ c \mapsto c' }{(\texttt{If}\ c\ t\ e) \mapsto (\texttt{If}\ c'\ t\ e) }&(1)\\\\
    \dfrac{ }{(\texttt{If}\ \texttt{True}\ t\ e) \mapsto t }&(2)\\\\
    \dfrac{ }{(\texttt{If}\ \texttt{False}\ t\ e) \mapsto e }&(3)
\end{gather}
$$
1. Show the full evaluation of the term (If True (If True False True) False). (5 marks)  

$$
\begin{align*}
&\text{(If True (If True False True) False)} \\
&\mapsto \text{If True False True (2)}\\
&\mapsto \text{False (2)}
\end{align*}
$$
<hr>
2. Define an equivalent big-step semantics for L. (5 marks)  

We define:
A set of evaluable expressions T 
A set of values V
A relation ⇓ ⊆ E × V
T is the set of all closed expressions {t | t ok} and V is the set {True, False}.

$$
\begin{gather}
\dfrac{}{\text{$v$\Downarrow $v$}}\quad&(L_1)\\\\
\dfrac{\text{ $t_1 \Downarrow$ True \quad$t_2 \Downarrow v_2$}}{\text{(If $t_1$ then $t_2$ else $t_3 )\Downarrow v_2$ }}&(L_2)\\\\
\dfrac{ \text{ $t_1 \Downarrow$ False \quad$t_3 \Downarrow v_3$}}{\text{(If $t_1$ then $t_2$ else $t_3 )\Downarrow v_3$ }}&(L_3)
\end{gather}
$$

<hr>
3.

Prove that if $e \Downarrow v$ then $e \stackrel{\star}{\mapsto} v$, where $\Downarrow$ is the big-step semantics you defined in the previous question, and $\stackrel{\star}{\mapsto}$ is the reflexive and transitive closure of $\mapsto$. Use rule induction on $e \Downarrow v$.


## Assumed Rules
$$
\dfrac{}{e \stackrel{\star}{\mapsto} e}refl
\quad
\dfrac{e \mapsto e' \quad e' \stackrel{\star}{\mapsto} e''}
{e \stackrel{\star}{\mapsto} e''}trans


$$



## If $e \Downarrow v$ then $e \stackrel{\star}{\mapsto} v$
#### Base Case $(e=v)$, from (A)
We must show that $v\stackrel{\star}{\mapsto} v$, obvious by rule refl.

#### Inductive Case $(e\ =\ (If\ t_1\ then\ t_2\ else\ t_3))$, from (B)

We know that $t_1 \Downarrow True$ and $t_2 \Downarrow v_2$, which gives us the inductive hypotheses:
- $IH_1 - t_1 \stackrel{\star}{\mapsto} True$
- $IH_2 - t_2 \stackrel{\star}{\mapsto} v_2$

Showing our overall goal:
$$
\begin{align*}
\text{(If $t_1$ then $t_2$ else $t_3$)}
&\stackrel{\star}{\mapsto}\text{(If True then $t_2$ else $t_3$)}&\text{($IH_1$ with 1)}\\
&\stackrel{\star}{\mapsto}t_2 &(2)\\
&\stackrel{\star}{\mapsto}\text{$v_2$} &(IH_2)\\

\end{align*}
$$

#### Inductive Case $(e\ =\ (If\ t_1\ then\ t_2\ else\ t_3))$, from (C)

We know that $t_1 \Downarrow False$ and $t_3 \Downarrow v_3$, which gives us the inductive hypotheses:
- $IH_1 - t_1 \stackrel{\star}{\mapsto} False$
- $IH_2 - t_3 \stackrel{\star}{\mapsto} v_3$

Showing our overall goal:
$$
\begin{align*}
\text{(If $t_1$ then $t_2$ else $t_3$)}
&\stackrel{\star}{\mapsto}\text{(If False then $t_2$ else $t_3$)}&\text{($IH_1$ with 1)}\\
&\stackrel{\star}{\mapsto}t_3 &(3)\\
&\stackrel{\star}{\mapsto}\text{$v_3$} &(IH_2)\\

\end{align*}
$$

Thus, by mathematical induction, we have shown one direction of the equivalence.


## If $e \stackrel{\star}{\mapsto} v$ then $e \Downarrow v$ 
Doing rule induction on the assumption $e \stackrel{\star}{\mapsto} v$  leads to two cases.
#### Base case $(e=v)$, from refl
We know that $v \Downarrow v$, from rule (A).

#### Inductive case ($e↦e'$ and $e \stackrel{\star}{\mapsto} v$), from trans
We have the inductive hypothesis that $e'\Downarrow v$, so it suffices to prove the following lemma in order to discharge this case.
$$\dfrac{s \mapsto s'\quad s' \Downarrow v}{s \Downarrow v}$$


#### Transitive Lemma: If $e↦e'$ and $e'⇓v$ then $e⇓v$
Written as a logical statement, this lemma is:
$$∀v. (e↦e')∧(e'⇓v)⇒e⇓v$$
Equivalently, this can be stated as:
$$(e↦e')⇒(∀v. e′⇓v)⇒(e⇓v)$$
This formulation lets us proceed by rule induction on the assumption $e↦e'$, proving for each case for any arbitrary v:
$$∀v. \dfrac{e'⇓v}{e⇓v}$$

#### Base Case 1, from rule (2)
Here $e = \text{(If True t e)}$ and $e' = t$.
We have to show that $e ⇓ v$ assuming that $e' ⇓ v$.
The only way that assumption could hold, looking at the rules of ⇓, is if $v = t$ from rule A.
Therefore we must show that $(\text{If True t e}) ⇓ t$, which is trivial from A and B.

#### Base Case 2, from rule (3)
Here $e = \text{(If False t e)}$ and $e' = \text{e}$.
We have to show that $e ⇓ v$ assuming that $e' ⇓ v$.
The only way that assumption could hold, looking at the rules of ⇓, is if $v =\text{e}$ from rule A.
Therefore we must show that $\text{(If True t e) ⇓ e}$, which is trivial from A and B.

#### Inductive Case, from rule (1)
Here $e = \text{(If c t e)}$ and $e' = \text{(If c}'\text{ t e)}$. We know that $c↦c'$, giving the inductive hypothesis that:

$$∀v. \dfrac{c'⇓v}{c⇓v}IH$$

We must show that $e ⇓ v$ assuming that $e' ⇓ v$.
Looking at the rules for ⇓, the only way that $e' ⇓ v$ could hold is if there is some $v_x$ such that 
$\text{c}'⇓v_x$ and $\text{t} ⇓ v_t$ and $\text{e} ⇓ v_e$. (which can be proven by rule B and C). 

Hence by the inductive hypothesis, we have that $c⇓v_x$. Therefore, $e ⇓ v$ as required.


# <hr><hr>

# Part C (15 marks)  
1. Define a recursive compilation function $c : B → L$ which converts expressions in $B$ to expressions in $L$. (5 marks)  

$$\begin{align}
c(\textsf{Not} \; x) &= \text{If\ $c(x)$\ then\ False\ else\ True}&(C_1)\\\\
c(\textsf{And} \; x \; y) &= \text{If $c(x)$ then $c(y)$ else False}&(C_2)\\\\
c(\textsf{True}) &= True&(C_3)\\\\
c(\textsf{False}) &= False&(C_4)
\end{align}
$$
<hr>

2. Prove that for all $e, e ⇓ v$ implies $c(e) ⇓ v$, by rule induction on the assumption that $e ⇓ v$. (10 marks)

For all proofs of induction, I have abbreviated $True \implies \mathsf{T}\ and\ False \implies \mathsf{F}$.

### Rule (1)
From (1), we declare $e =\mathsf{Not}\ x$, $v = \mathsf{F}$ and the assumption $x \Downarrow \mathsf{T}$.
Hence the statement above we conclude our inductive hypothesis:
$$
\begin{align*}
c(x)&\Downarrow \mathsf{T}&\quad(I.H.)
\end{align*}

$$

We can now prove that $c(e) \Downarrow v$, or in other words $c(\mathsf{Not}\ x)=\mathsf{F}$.
$$
\begin{align*}

\dfrac{\dfrac{}{c(x)\Downarrow \mathsf{T}}(I.H.)\quad\dfrac{}{\mathsf{F}\Downarrow \mathsf{F}}(B_6)}
{
\dfrac{\text{(If $c(x)$ then $\mathsf{F}$ else $\mathsf{T}$)\ $\Downarrow \mathsf{F}$ }}
{
c(\mathsf{Not}\ x)  \Downarrow \mathsf{F}
}(C_1)
}(L_2)

\end{align*}
$$

### Rule (2)
From (2), we declare $e =\mathsf{Not}\ x$, $v = \mathsf{T}$ and the assumption $x \Downarrow \mathsf{F}$.

Hence the statement above we conclude our inductive hypothesis:
$$
\begin{align*}
c(x)&\Downarrow \mathsf{F}&\quad(I.H.)
\end{align*}

$$

We can now prove that $c(e) \Downarrow v$, or in other words $c(\mathsf{Not}\ x)=\mathsf{T}$.
$$
\begin{align*}

\dfrac{\dfrac{}{c(x)\Downarrow \mathsf{F}}(I.H.)\quad\dfrac{}{\mathsf{T}\Downarrow \mathsf{T}}(B_5)}
{
\dfrac{\text{(If $c(x)$ then $\mathsf{F}$ else $\mathsf{T}$)\ $\Downarrow \mathsf{T}$ }}
{
c(\mathsf{Not}\ x)  \Downarrow \mathsf{T}
}(C_1)
}(L_2)

\end{align*}
$$


### Rule (3)
From (3), we declare $e =\mathsf{And}\ x\ y$, $v = \mathsf{F}$ and the assumption $x \Downarrow \mathsf{F}$.

Hence the statement above we conclude our inductive hypotheses:
$$
\begin{align*}
c(x)&\Downarrow\mathsf{F} &\quad(I.H.)
\end{align*}
$$

We can now prove that $c(e) \Downarrow v$, or in other words $c(\mathsf{And}\ x\  y)=\mathsf{F}$.
$$
\begin{align*}
\dfrac{

\dfrac{}{c(x)\Downarrow \mathsf{F}}(I.H_1)\quad
\dfrac{}{\mathsf{F}\Downarrow \mathsf{F}}(B_6)}

{
\dfrac{\text{(If $c(x)$ then $c(y)$ else $\mathsf{F}$)\ $\Downarrow \mathsf{F}$ }}
{
c(\mathsf{And}\ x\ y)  \Downarrow \mathsf{F}
}(C_2)
}(L_3)

\end{align*}
$$

### Rule (4)
For this proof, I have renamed the value $v$ from the rule, as $\mathsf{v_k}$.

From (4), we declare $e =\mathsf{And}\ x\ y$, $v = \mathsf{v_k}$ and the assumptions $x \Downarrow \mathsf{T}$ and $y \Downarrow \mathsf{v_k}$.

Hence the statement above we conclude our inductive hypotheses:
$$
\begin{align*}
c(x)&\Downarrow \mathsf{T} &\quad(I.H_1)
\\
\\
c(y)&\Downarrow \mathsf{v_k} &\quad(I.H_2)
\end{align*}

$$

We can now prove that $c(e) \Downarrow v$, or in other words $c(\mathsf{And}\ x\ y)=\mathsf{v_k}$.
$$
\begin{align*}
\dfrac{

\dfrac{}{c(x)\Downarrow \mathsf{T}}(I.H_1)\quad
\dfrac{}{c(y)\Downarrow \mathsf{v_k}}(I.H_2)}

{
\dfrac{\text{(If $c(x)$ then $c(y)$ else $\mathsf{F}$)\ $\Downarrow \mathsf{v_k}$ }}
{
c(\mathsf{And}\ x\ y)  \Downarrow \mathsf{v_k}
}(C_2)
}(L_2)

\end{align*}
$$

### Rule (5)
From (5), we declare $e = \mathsf{T}$, $v = \mathsf{T}$.
We can now prove that $c(e) \Downarrow v$, or in other words $c(\mathsf{T}) \Downarrow \mathsf{T}$.

$$
\dfrac{}{\dfrac{T \Downarrow T}{c(T) \Downarrow T}}
$$
### Rule (6)
From (6), we declare $e = \mathsf{F}$, $v = \mathsf{F}$.
We can now prove that $c(e) \Downarrow v$, or in other words $c(e) \Downarrow \mathsf{F}$.
$$
\dfrac{}{\dfrac{F \Downarrow F}{c(F) \Downarrow F}}
$$



# <hr><hr>

# Part D.
1. Here is a term in $\lambda$-calculus:
$$ (\lambda n.\ \lambda f.\ \lambda x.\ (n\ f\ (f\ x)))\ (\lambda f.\ \lambda x.\ f\ x) $$
a) Fully β-reduce the above λ-term. Show all intermediate beta reduction steps. (5 marks)
$$
\begin{align*}
(\lambda n.\ \lambda f.\ \lambda x.\ (n\ f\ (f\ x)))\ (\lambda f.\ \lambda x.\ f\ x)
&\mapsto_\beta\lambda f.\ \lambda x.\ ((\lambda f.\ \lambda x.\ f\ x) \ f\ (f\ x))&\text{[On $n$]}\\
&\equiv_\alpha\lambda f.\ \lambda x.\ ((\lambda f'.\ \lambda x'.\ f'\ x') \ f\ (f\ x))&\text{[$f\mapsto\ f'$, $x\mapsto\ x'$]}\\
&\mapsto_\beta\lambda f.\ \lambda x.\ ((\ \lambda x'.\ f\ x' )\ (f\ x))\quad&\text{[On $f'$]}\\
&\mapsto_\beta\lambda f.\ \lambda x.\ f\ (f\ x)\quad \blacksquare &\text{[On $x'$]}
\end{align*}
$$
<hr>

b) Identify an η-reducible expression in the above (unreduced) term. (5 marks)

We can reduce the unreduced expression using $\eta$-reduction on $x$.
$$
\begin{align*}
(\lambda n.\ \lambda f.\ \lambda x.\ (n\ f\ (f\ x)))\ (\lambda f.\ \lambda x.\ f\ x)
&\mapsto_\eta(\lambda n.\ \lambda f.\ \lambda x.\ (n\ f\ (f\ x)))\ (\lambda f.\ f)
\end{align*}
$$
<hr>
### For question 2 and 3, I will shorthand $(λx. λy. x) \implies \mathbf{T}$ and $(λx. λy. y) \implies \mathbf{F}$.

2. Recall that in λ-calculus, booleans can be encoded as binary functions that return one of their arguments:  
$$\begin{align*}\mathbf{T} ≡ (λx. λy. x)\\  
\mathbf{F} ≡ (λx. λy. y)  \end{align*}$$
Either via L or directly, define a function d : B → λ which converts expressions in B to λ-calculus. (5 marks)




$$\begin{align*}
d(\textsf{Not} \; x) &= (\lambda x. x\ \mathbf{F}\ \mathbf{T})\ d(x)&(D_1)\\\\
d(\textsf{And} \; x \; y) &= (\lambda a. \lambda b.\ a\ b\ a)\ d(x)\ d(y)&(D_2)\\\\
d(\textsf{True}) &= \mathbf{T}&(D_3)\\\\
d(\textsf{False}) &= \mathbf{F}&(D_4)
\end{align*}
$$

3. Prove that for all e such that $e ⇓ v$ it holds that $d (e) \equiv_{\alpha\beta\eta} v'$, where $v'$ is the  
λ-calculus encoding of v.

### Rule (1)
From (1), we declare $e =\mathsf{Not}\ x$, $v = \mathsf{False}$ and the assumptions $x \Downarrow \mathsf{True}$.
From the statement above we have our inductive hypothesis:
$$
\begin{align*}
d(x)&=d(True)&\\
&=\mathbf{T}&(I.H.)
\end{align*}
$$
We also compute $v'$

$$
\begin{align*}
v'&=d(v)&\\
&=d(False)\\
&=\mathbf{F}
\end{align*}
$$

We can now prove that $d(e) \equiv_{\alpha\beta\eta} v'$, or in other words $d(\mathsf{Not} \ x) \equiv_{\alpha\beta\eta} \mathsf{F}$.A
$$
\begin{align*}
d(\mathsf{Not}\ x)
&=(\lambda x. x\ \mathbf{F}\ \mathbf{T}) \ d(x)&(D_1)\\
&=(\lambda x. x\ \mathbf{F}\ \mathbf{T}) \ \mathbf{T} &(From \ I.H)\\
&\equiv_{\alpha\beta\eta}\mathbf{T}\ \mathbf{F}\ \mathsf{T}\\
&\equiv_{\alpha\beta\eta}\mathbf{F} &\blacksquare\\
\end{align*}
$$

### Rule (2)
From (2), we declare $e =\mathsf{Not}\ x$, $v = \mathsf{True}$ and the assumptions $x \Downarrow \mathsf{False}$.
From the statement above we have our inductive hypothesis:
$$
\begin{align*}
d(x)&=d(False)&\\
&=\mathbf{F}&(I.H.)
\end{align*}
$$
We also compute $v'$

$$
\begin{align*}
v'&=d(v)&\\
&=d(True)\\
&=\mathbf{T}
\end{align*}
$$

We can now prove that $d(e) \equiv_{\alpha\beta\eta} v'$, or in other words $d(\mathsf{Not} \ x) \equiv_{\alpha\beta\eta} \mathsf{T}$.
$$
\begin{align*}
d(\mathsf{Not}\ x)
&=(\lambda x. x\ \mathbf{F}\ \mathbf{T}) \ d(x)&(D_1)\\
&=(\lambda x. x\ \mathbf{F}\ \mathbf{T}) \ \mathbf{F} &(From \ I.H)\\
&\equiv_{\alpha\beta\eta}\mathbf{F}\ \mathbf{F}\ \mathsf{T}\\
&\equiv_{\alpha\beta\eta}\mathbf{T} &\blacksquare\\
\end{align*}
$$
### Rule (3)
From (3), we declare $e =\mathsf{And}\ x\ y$, $v = \mathsf{False}$ and the assumptions $x \Downarrow \mathsf{False}$.
From the statement above we have our inductive hypotheses:
$$
\begin{align*}
d(x)&=d(False)&\\
&=\mathbf{F}&(I.H.)\\\\
\end{align*}
$$
We also compute $v'$

$$
\begin{align*}
v'&=d(v)&\\
&=d(False)\\
&=\mathbf{F}
\end{align*}
$$

We can now prove that $d(e) \equiv_{\alpha\beta\eta} v'$, or in other words $d(\mathsf{And} \ x\ y) \equiv_{\alpha\beta\eta} \mathsf{F}$.
$$
\begin{align*}
d(\mathsf{And}\ x\ y)
&=(\lambda a. \lambda b.\ a\ b\ a)\ d(x)\ d(y)&(D_2)\\
&=(\lambda a. \lambda b.\ a\ b\ a)\ \mathbf{F}\ d(y)&(From \ I.H)\\
&\equiv_{\alpha\beta\eta}(\lambda b\ \mathbf{F}\ b\ \mathsf{F})\ d(y)\\
&\equiv_{\alpha\beta\eta}\mathbf{F}\ d(y)\ \mathbf{F}\\
&\equiv_{\alpha\beta\eta}\mathbf{F} &\blacksquare\\
\end{align*}
$$


### Rule (4)
For this proof, I have renamed the value $v$ from the rule, as $\mathbf{v_k}$.
From (4), we declare $e =\mathsf{And}\ x\ y$, $v = \mathbf{v_k}$ and the assumptions $x \Downarrow \mathsf{True}$ and $y \Downarrow \mathbf{v_k}$.
From the statement above we have our inductive hypotheses:
$$
\begin{align*}
d(x)&=d(True)&\\
&=\mathbf{T}&(I.H_1.)\\\\
d(y)&=d(\mathbf{v_k})&(I.H_2.)
\end{align*}
$$
We also compute $v'$

$$
\begin{align*}
v'&=d(\mathbf{v_k})&\\
\end{align*}
$$

We can now prove that $d(e) \equiv_{\alpha\beta\eta} v'$, or in other words $d(\mathsf{And} \ x\ y) \equiv_{\alpha\beta\eta} d(\mathbf{v_k})$.
$$
\begin{align*}
d(\mathsf{And}\ x\ y)
&=(\lambda a. \lambda b.\ a\ b\ a)\ d(x)\ d(y)&(D_2)\\
&=(\lambda a. \lambda b.\ a\ b\ a)\ \mathbf{T}\ d(\mathbf{v_k})&(From \ I.H_1\ and\ I.H_2.)\\
&\equiv_{\alpha\beta\eta}(\lambda b\ \mathbf{T}\ b\ \mathbf{T})\ d(\mathbf{v_k})\\
&\equiv_{\alpha\beta\eta}\mathbf{T}\ d(\mathbf{v_k})\ \mathbf{T}\\
&\equiv_{\alpha\beta\eta}d(\mathbf{v_k}) &\blacksquare\\
\end{align*}
$$

### Rule (5)
From (5), we declare $e = True$ and $v=True$.
We also compute $v'$
$$
\begin{align*}
v'&=d(True)\\
&=\mathbf{T}
\end{align*}
$$
We can now prove that $d(e) \equiv_{\alpha\beta\eta} v'$, or in other words $d(\mathsf{True} ) \equiv_{\alpha\beta\eta} \mathbf{T}$.
$$
\begin{align}
d(True) &\equiv_{\alpha\beta\eta} \mathbf{T} &(D_3)
\end{align}
$$

### Rule (6)
From (6), we declare $e = False$ and $v=False$.
We also compute $v'$
$$
\begin{align*}
v'&=d(False)\\
&=\mathbf{F} &(D_4)
\end{align*}
$$
We can now prove that $d(e) \equiv_{\alpha\beta\eta} v'$, or in other words $d(\mathsf{False} ) \equiv_{\alpha\beta\eta} \mathbf{F}$.
$$
\begin{align}
d(False) &\equiv_{\alpha\beta\eta} \mathbf{F} &(D_3)
\end{align}
$$


<hr>
4. Suppose we added unary local function definitions to our language $\mathcal{P}$. Here's an example in concrete syntax:
$$
  \begin{array}{l}
    \mathsf{let} \\
    \;\;\mathit{g}(\mathit{x}) = \neg\mathit{x} \\
    \mathsf{in} \\
    \;\; \mathit{g}(\mathsf{True})\\
    \mathsf{end}
  \end{array}
$$
We limit ourselves to non-recursive bindings (meaning functions can't call themselves), and first-order functions (meaning functions require boolean arguments).

a) Extend the abstract syntax for $\mathcal{B}$ from question A.3 so that it supports the features used in the above example. Use first-order abstract syntax with explicit strings. You don't have to extend the parsing relation. (5 marks)

We extend B to 
$$
\begin{align}
B ::&=\ &\mathsf{True}\\
&|\ &\mathsf{False}\\
&|\ &\mathsf{Not\ B}\\
&|\ &\mathsf{And\ B\ B}\\
&|\ &\mathsf{Func\ F\ B}\\
&|\ &\mathsf{Var\ M}\\
&|\ &\mathsf{Let\ F\ B\ B\ in\ B\ End}
\end{align}
$$
For my additions:
Func F B takes in two arguments, F is the function name and B is the variable.
Var M takes in one argument, where M is a variable.
Let F B B B takes in four arguments, F is the name of the function, the first B is the assigned variable for F, the second B is the replacement expression, and the third B is the expression we apply the function. 
An example is Let "g" (Var "x") (Not "x") (F "g" True)

b) Define a scope-checking judgement, similar to the $\mathbf{ok}$ judgement from the lectures. It should check (a) that all names of variables and functions are used only within their scopes; and (b) that names used in variable (or function) position are indeed the names of variables (or functions). Hence, the following expressions should both be rejected:

  
$$

\begin{array}{l}

\mathsf{let} \\

\;\;\mathit{f}(\mathit{x}) = \neg\mathit{x} \\

\mathsf{in} \\

\;\; \mathit{f}(\mathit{x})\\

\mathsf{end}

\end{array}

\quad 
\begin{array}{l}

\mathsf{let} \\

\;\;\mathit{f}(\mathit{x}) = \neg\mathit{x} \\

\mathsf{in} \\

\;\; \mathit{f}(\mathit{f})\\

\mathsf{end}

\end{array}

\quad

\begin{array}{l}

\mathsf{let} \\

\;\;\mathit{f}(\mathit{x}) = \mathit{x}(\mathsf{True}) \\

\mathsf{in} \\

\;\; \mathit{f}(\mathsf{False})\\

\mathsf{end}

\end{array}    


  
$$
    The following are examples of things that should be accepted: nullary definitions, nested definitions, and shadowed definitions.
$$
\begin{array}{l}

\mathsf{let} \\

\;\;\mathit{f}(\mathit{x}) =\\



\quad\mathsf{let} \\

\quad\;\;\mathit{g}(\mathit{y}) = \neg\mathit{x}\wedge\mathit{y} \\

\quad\mathsf{in} \\

\quad\;\; \mathit{g}(\mathit{x}) \wedge \neg\mathit{g}(\mathit{x})\\

\quad\mathsf{end}\\

\mathsf{in} \\

\;\; \mathit{f}(\mathsf{False})\\

\mathsf{end}

\end{array}

\quad

\begin{array}{l}

\mathsf{let} \\

\;\;\mathit{f}(\mathit{x}) = \mathit{x}(\mathsf{True}) \\

\mathsf{in} \\

\quad\mathsf{let} \\

\quad\;\;\mathit{f}(\mathit{x}) = \mathit{f}(\mathit{x}) \\

\quad\mathsf{in} \\

\quad\;\; \mathit{f}(\mathsf{True})\\

\quad\mathsf{end}\\

\mathsf{end}

\end{array}    
$$
Note that the latter example is not a recursive call. (10 marks)

 It should check 
 (a) that all names of variables and functions are used only within their scopes
 (b) that names used in variable (or function) position are indeed the names of variables (or functions).

$$
\begin{gather}
&\dfrac{}{\Gamma \vdash True\ \mathbf{ok}}\\\\
&\dfrac{}{\Gamma \vdash False\ \mathbf{ok}}\\\\
&\dfrac{\Gamma \vdash e_1\ \mathbf{ok}}{\Gamma \vdash \mathsf{Not}\ (e_1)\ \mathbf{ok}}\\\\
&\dfrac{\Gamma \vdash e_1\ \mathbf{ok}\quad\Gamma \vdash e_2\ \mathbf{ok}}{\Gamma \vdash \mathsf{And}\ (e_1\ e_2)\ \mathbf{ok}}\\\\
&\dfrac{(x\ bound)\in\Gamma}{\Gamma \vdash (Var\ x)\ \mathbf{ok}}\\\\
&\dfrac{(f\ bound)\in\Gamma\quad\Gamma\vdash e_1\  \mathbf{ok}}{\Gamma \vdash (Func\ f\ e_1)\ \mathbf{ok}}\\\\
&\dfrac{(x\ bound), \Gamma\vdash e_1\quad(f\ bound) ,\Gamma\vdash e_2\  \mathbf{ok}}{\Gamma \vdash (Let\ f\ x\ e_1\ e_2)\ \mathbf{ok}}\\\\
\end{gather}

$$