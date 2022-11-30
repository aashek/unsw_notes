
b) Define a scope-checking judgement, similar to the **ok** judgement from the lectures. It should check (a) that all names of variables and functions are used only within their scopes; and (b) that names used in variable (or function) position are indeed the names of variables (or functions). Hence, the following expressions should both be rejected:  
```
let  
	f (x ) = ¬x  
in  
	f (x )  
end 

x is a free variable (unbound)
``` 
```
let  
	f (x ) = ¬x  
in  
	f (f )  
end

we need some way to differentiate functions from variable binds.
```  
```
let  
	f (x ) = x (True)  
in  
	f (False)  
end
when defining, we need some way to invalidate applying a variable as a function
```  
The following are examples of things that should be accepted: nested definitions, and shadowed definitions.  
```
let  
	f (x ) =  
		let  
			g(y) = ¬x ∧ y  
		in  
			g(x ) ∧ ¬g(x )  
		end  
in  
	f (False)  
end  
```
```
let  
	f (x ) = x  
in  
	let  
		f (x ) = f (x )  
	in  
		f (True)  
	end  
end 
``` 
Note that the latter example is not a recursive call. (10 marks)
$$
\begin{align*}
\frac{}{\Gamma \vdash True\ \textbf{ok}} &\qquad \frac{}{\Gamma \vdash False\ \textbf{ok}}\\\\



\frac{\Gamma \vdash e_{1} \textbf{ ok}}
{\Gamma \vdash \text{Not } e_{1} \textbf{ ok}}
&\qquad
\dfrac{
\Gamma \vdash e_{1}\textbf{ ok} \quad \Gamma \vdash e_2\textbf{ ok}
}{\Gamma \vdash \text{And } e_{1}\ e_{2} \textbf{ ok}}\\\\
\frac{}{\Gamma \vdash f(x)\textbf{ ok}}
&\qquad
 
\frac{\text{x bound}, \Gamma \vdash e_{1}\textbf{ ok}\quad \text{f bound},\Gamma \vdash e_2\textbf{ ok}}
{\text{$\Gamma\vdash$ Let f x $e_1$ $e_2$}\textbf{ ok}}\\ \\


\dfrac{\text{f bound}\in\Gamma \quad \Gamma\vdash e_{1} \textbf{ ok}}{\Gamma\vdash \text{Func f $e_1$}\textbf{ ok}} &\qquad
\dfrac{\text{x bound} \in \Gamma}{\Gamma \vdash \text{Var x}\textbf{ ok}}

\end{align*}
$$

$$
\dfrac{
\dfrac{}{\vdash}



}
{\text{let f(x)= let g(y) = $\neg$x $\wedge$ y in g(x) $\wedge$ $\neg$g(x) end in f(False) end}}
$$

$$
\dfrac{

\dfrac{

\dfrac{}{\text{x}\vdash \text{Var x}}

}{\text{x}\vdash \text{Not (Var x)}}
\quad

\dfrac{\vdash \text{True}}{\text{f}\vdash\text{f(True)}}

}{\vdash \text{Let\ f(Var x) = Not\ x\ in\ f(True)\ end}}
$$
f = (\\la x. -> x)

$$\dfrac{

\dfrac{

\dfrac{

\dfrac{\dfrac{}{\text{x,y}\vdash(V x)\textbf{ ok}}}{\text{x,y}\vdash \neg (V x)\textbf{ ok}}
\quad
\dfrac{}{\text{x,y}\vdash (V y)\textbf{ ok}}

}{\text{x,y}\vdash \text{$\neg$(V x) $\wedge$ (V y)}\textbf{ ok}} 
\quad
\dfrac{

\dfrac{
\dfrac{}{\text{x,g}\vdash V x\textbf{ ok}}}{\text{x,g}\vdash g((V x))\textbf{ ok}}
\quad

\dfrac{

\dfrac{
\dfrac{}{\text{x}\vdash (V x)\textbf{ ok}}
}{\text{x,g}\vdash g((V x))\textbf{ ok}}
}{\text{x,g}\vdash \neg g((V x))\textbf{ ok}}

}{\text{x,g}\vdash g((V x)) \wedge \neg g((V x))\textbf{ ok}}

}{\text{x} \vdash\text{let g(y) = $\neg$(V x) ∧ (V y) in g((V x)) ∧ $\neg$g((V y)) end}\textbf{ ok}}
\quad
\dfrac{\dfrac{}{\vdash\text{False}\textbf{ ok}}}{\text{f}\vdash\text{f (False)}\textbf{ ok}}

}
{\text{let  f (x ) =  let  g(y) = $\neg$(V x) ∧ (V y)  in  g((V x)) ∧ $\neg$g((V x)  end  in  f (False)  end}\textbf{ ok}}
$$ 
