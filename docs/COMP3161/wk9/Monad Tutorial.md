```toc
```


## Abstract Nonsense

A monad is a type constructor m, with two functions:
```
return "return"

has the form

a -> m a

```

```
>>= "bind"

m a -> (a -> m b) -> m b

where a and b are type variables (universally quantified)
```

return is the left and right identity laws
```
// if i have m and that is passed into return, i get m
// if i have a value and pass that into a function, i get f (x)

m >>= return = m
return x >>= m = m x
```

bind abstracts computation via the >>= command

Take for a calculator we want the following behaviour

plus e1 e2
eval left return if error
eval right return if error.
return left + right

```haskell


Plus ::
Plus e1 e2 =
	case eval e1 of
		Nothing -> Nothing
		Just x ->
			(
			case eval e2
				Nothing -> Nothing
				Just y -> x + y
			)
```

We improve this code using two standard librarys in haskell.
1. Maybe monad 
This has return and bind. but it also stops running and returns nothing if error.
2. do notation
do is syntactic sugar for run this line, if it fails then return the failure

```haskell

calc'' (Num n) = return n

calc'' (Plus e1 e2) =
do 
	n <- eval e1 -- stops running at this point
	m <- eval e2 -- need the context of e1 essentially
	return $ n + m
 ```









TC Monad
- Makes error handling simplier
- Generates fresh names we dont have to worry about


