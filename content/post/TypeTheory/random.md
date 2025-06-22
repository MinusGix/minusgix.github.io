+++
date = '2025-06-07T10:05:54-04:00'
draft = true
title = 'Random'
math = true
+++

*R*a**n**d*o***m** Terminology!

This is a megapost for certain concepts that come up often in Type Theory, but don't necessarily deserve a post all on their own, or at least have a short enough conceptual handle for a short paragraph or two to be enough of a reference.  

## Contravariance
A Contravariant functor, $F : C^{op} \to Set$    
If you think of $C$ as your "contexts" or "stages of transformation", then the contravariance means that as you go to more informative contexts, you can always transport backwards.  
Like, for example, you prove a property in a stronger context, you can weaken it to work in a more general one.   
Like, as a trivial example, you prove $P(x)$ in a context $\Gamma, x : A$, you can transport it to a context $\Gamma, x : A, y : B$ by just adding the new variable $y : B$ to the context.  

If you have some function $g : A \to B$, then $F(g) : F(B) \to F(A)$, it reverses the direction of the arrow and maps the types.  
For example, function types themselves.  
If you have $g : A \ to B$, then $(B \to R) \to (A \to R)$  
That is, if you are given a function $h : B \to R$ that takes a $B$ and gives you an $R$, you can then produce a new function $j : A \to R$ that takes an $A$ and gives you an $R$ by composing $h$ with $g$. This is similar to transitivity but defined in an odder manner.

## Covariance
A Covariant functor, $F : C \to Set$  
This preserves arrow directions.  
If you have some other function, $g : A \to B$ then $F(g) : F(A) \to F(B)$. That is, it merely maps the input/output types.  

The most clear example of this is that of `List` with a `map` function. If you have a function $\text{Int} \to \text{String}$ then you get a new function $\text{List Int} \to \text{List String}$ by just mapping the input/output types.  
(or, rather, having a rule for spreading that individual function out over each element)

## Mixed Variance
You can end up with mixed variance.  
Like with $\text{Hom} : C^{op} \times C \to Set$ is intuitively contravariant in the first argument, covariant in the second.  
