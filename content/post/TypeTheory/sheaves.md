+++
date = '2025-05-19T01:29:55-04:00'
draft = true
title = 'Sheaves'
categories = ["Type Theory"]
tags = ["Type Theory", "Sheaves"]
math = true
+++

## Basic
Sheaves allow you to systematically track local information and also how it glues together into global information, where it agrees where the regions overlap.

Let's say you have some topological space $X$, your "domain", and you want to track some information with *each* open subset of $X$.  

We add two conditions:

Where $U \subseteq X$ is some open set within $X$.  

**Locality**: If we have some data on an open set $U$, and it restricts to "zero" on every small neighborhood covering $U$, then the original data must be "zero" as well.   

> [!note]
> **Analogy**: This is similar to saying that if a function is zero everywhere locally, then it must be zero globally.
> **Formal**: $\forall s,t \in \mathcal{F}(U), \forall i \in I, s\mid_{U_i} = t\mid_{U_i} \implies s = t$
> That is, for every two pieces of data, if they agree on every small neighborhood covering $U$ (that indexing, $U_i$), then they are equivalent.  
> It is not required to only consider zero, but it is a common example.

**Gluing**: If we have compatible data on overlapping open sets, you can uniquely glue them together into the data on the union.

> [!note]
> **Formal**: 
> Fix some family of open sets $U_i$, where $i,j \in I$  
> For specific data, $s_i \in \mathcal{F}(U_i)$ for each open set $U_i$  
> If $s_i\mid_{U_i \cap U_j} = s_j \mid_{U_i \cap U_j}$ for all $i, j \in I$,
> Then there exists a unique data $s \in \mathcal{F}(U)$ where $U = \bigcup_{i \in I} U_i$ where $\forall i,\ s\mid_{U_i} = s_i$
> 


As well, a Sheaf is also a Presheaf which has some minor constraints. See [here](#presheaves)

This data could be many things:

> [!note]
> **Continuous functions**
> For each open set $U \subseteq X$, we have that $\mathcal{F}(U) = \mathcal{C}(U) = \{\text{continuous functions}\ f : U \to \R \}$  
> That is, we can acquire all the continuous functions (to the real numbers) defined on each open set.
>
> *Locality*: $f, g \in \mathcal{C}(U)$ means that $f : U \to \R$ and $g : U \to R$ are two continuous functions associated with the open set $U$. Any two that can be defined over that open.  
> If they aree in every small neighborhood, then they are the same function.
>
> *Gluing*: If you have continuous functions $f_i$ which overlap, *and* that they agree on the intersections, then you can get a unique continuous function on $\cup U_i$

> [!note]
> **Solutions to Differential Equations**
> Let an open $X \subseteq \R^n$ and consider $\frac{dy}{dx} = f(x, y)$ for some function $f$. 
> For each open $U \subseteq X$, let $S(U)$ be the set of solutions $y(x)$ to the equation on $U$.
> You can glue solutions that agree on overlaps to get solutions on larger domains.
>
> This neatly captures the local-to-global nature of differential equations.

> [!note]
> **Locally Constant Functions**
> A function $f : X \to \R$ is **locally constant** if for every point $x \in X$, there is an open neighborhood $U$ of $x$ such that $f$ is constant on $U$.
> This sheaf assigns $\mathcal{LC}(U) = \{f : U \to \R \mid f\ \text{is locally constant}\}$ as the data.
> On a connected open set $U$, every locally constant function is constant.  
> Though if they're disconnected, then the neighborhood can't "expand", and so you can have isolated parts with different values.




## Presheaves

TODO


## Summary
Sheaves:
- Associate data to each open set
  - That can be whole sets, so one way of viewing it is that there are multiple consistent pieces of data that can be associated with the same open set.
- Has a conception of "locality", that if the data agrees on all "small neighborhoods" then it must be the same data.
  - Intuitively, if they agree everywhere locally, there's no distinction between them.
-

Presheaves:

Sections:

Stalks:
