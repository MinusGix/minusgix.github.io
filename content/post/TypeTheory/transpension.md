+++
date = '2025-05-19T01:13:26-04:00'
draft = false
title = 'Transpension'
tags = ["Type Theory"]
categories = ["Type Theory"]
math = true
+++

**Topic**: [Transpension: The Right Adjoint to the Pi-type](https://arxiv.org/abs/2008.08533) by Andres Nuyts and Dominique Devriese.

**Abstract**:
> Presheaf models of dependent type theory have been successfully applied to model HoTT, parametricity, and directed, guarded and nominal type theory. There has been considerable interest in internalizing aspects of these presheaf models, either to make the resulting language more expressive, or in order to carry out further reasoning internally, allowing greater abstraction and sometimes automated verification. While the constructions of presheaf models largely follow a common pattern, approaches towards internalization do not. Throughout the literature, various internal presheaf operators (\surd, \Phi/\mathsf{extent}, \Psi/\mathsf{Gel}, \mathsf{Glue}, \mathsf{Weld}, \mathsf{mill}, the strictness axiom and locally fresh names) can be found and little is known about their relative expressivenes. Moreover, some of these require that variables whose type is a shape (representable presheaf, e.g. an interval) be used affinely. We propose a novel type former, the transpension type, which is right adjoint to universal quantification over a shape. Its structure resembles a dependent version of the suspension type in HoTT. We give general typing rules and a presheaf semantics in terms of base category functors dubbed multipliers. Structural rules for shape variables and certain aspects of the transpension type depend on characteristics of the multiplier. We demonstrate how the transpension type and the strictness axiom can be combined to implement all and improve some of the aforementioned internalization operators (without formal claim in the case of locally fresh names).

## Introduction

Wow, the second blogpost and I'm talking about Transpension of all things.

Specifically, [Transpension: The Right Adjoint to the Pi-type](https://arxiv.org/abs/2008.08533) by Andres Nuyts and Dominique Devriese. This is the paper referred to by ND24, seen in some of Andreas' presentations like [https://www.math.uwo.ca/faculty/kapulkin/seminars/hottestfiles/Nuyts-2024-05-02-HoTTEST.pdf](https://www.math.uwo.ca/faculty/kapulkin/seminars/hottestfiles/Nuyts-2024-05-02-HoTTEST.pdf)

This paper came to my interest due to the mention in the slides linked above of using [MTT](./MultimodalTypeTheory.md) (Multimodal Type Theory) for 'variance', and MTras (Modal Transpension System) for substructural intervals.  
I like substructurality. I think it makes a type theory much nicer as a programming language, as such a nature better models the reality of programs (copying is not free) and allows expressing meaningful constraints directly without needing to abstract out.  


So, we'll take a look at Transpension, and see precisely what it gives us as a tool to work with. The paper is nontrivial to understand.  

The first way to look at it is that it takes multiple existing special-cases of useful features that have been discussed in Type Theory literature, and provides a general tool to specialize them.

<!-- TODO: Add a 'reminder' admonition kind that has a title. Maybe it should be on the side? -->
<!-- > [!note]+ Pi Types
> Tidbit! Pi types are simply 'forall'. -->

----

$\newcommand\tra{≬}\newcommand\Ty{\text{Ty}}\newcommand\I{\mathbb{I}}\newcommand\U{\mathbb{U}}$

## Pi-type
Before we even cover transpension, the new concept introduced by this paper, I find it important to (re)introduce the conception of Pi-type.

To put it most simply, as many readers will already know, a Pi-type is functionally a "forall" statement.  
$$\forall x : \R, x < x + 1$$
vs.
$$\Pi(x : \R), x < x + 1$$

Functionally these are the same, but we call it the Pi-type because (TODO: why?)

The typical Type Theory viewpoint of these is that $\Pi(x : \R), P(x)$ up there is *effectively* a function: "I take a real number, and return a proof that $P(x)$ holds for your specific $x$ value."  

However, an important tidbit here that may not be immediately obvious when thinking about for-all, is that a Pi-type is not necessarily restricted to just Propositions. You could very well have, for example,
$$\Pi(n : \N), \text{Array} n$$  
That is, it constructs an instance of a type for you. You give this a natural number, and you get a type back that depends on the natural number you gave it.

You can do very well thinking of Pi-types and forall as fancy functions. (TODO: are they equivalent to functions? where do they depart?)

But an important thing to remember is that we are calling this a Pi-type.  
As an example:
$$zeroes : \Pi(n : \N), \text{Array} n := [0, \dots^n, 0]$$
$$counting : \Pi(n : \N), \text{Array} n := [0, 1, 2, \dots, n]$$

Are both perfectly valid instances of the Pi-type.  

----

The Pi-type itself is effectively parameterized by two types. The input type, like $\N$ above, and the output type- but that output type can *depend* upon the value of the first input. This is part of the distinction from a typical conception of function, and is where dependent in dependent types comes from.

## Interval

This paper heavily uses intervals/shapes. See [intervals](./intervals.md) for an explanation, though yu should pick up on that to have a better idea of what is being talked about.

## Transpension

> [!note]
> **Transpension:**
> $$\tra[i] : \Ty(\Gamma) \to \Ty(\Gamma, i : \I)$$
> Transpension is defined as a type former. It takes in some type in the context and translates it into one which depends upon the interval variable $i$.  

This is a [right-adjoint](ncat:right-adjoint) to the Pi-type former:  
$$\Pi(i : \I) : \Ty(\Gamma, i : \I) \to \Ty(\Gamma)$

Remember our discussion about Pi-types before, that they take two types. The input type, and a second type which can depend on the value of the first. That is effectively what is being said here, with $i : \I$ simply being the first parameter like quantifying over an $n : \N$.  
$Ty(\Gamma, i : \I)$ is specifying the second type, which will be the type of the resulting value. It depends on the context and on the first value given. The last $\Ty(\Gamma)$, to be quite clear, is merely the resulting Pi-type that has been formed.  

Let's glance back at transpension.  
Okay, so it says $\tra[i]$- It depends on $i$ in some manner, though uses a different syntax. Square brackets rather than parentheses.  
$\Ty(\Gamma)$ so all it has is a type parameter and then it... returns a type that depends on $i : \I$?

You can functionally treat this as $\tra[i]$ *introducing* an $i$ into scope, that this type definition depends upon. You can also see why this is called a "right adjoint", it takes the resulting Pi type goes backwards effectively.

## MTraS
A core offering of this concept of Transpension is that it simplifies your definition of a type theory. From the rules of Transpension, one can define several kinds of special operators in a simpler manner, and linking back to this one concept.

MTraS is a type system that this paper constructs which features a transpension type, $\tra[u : \U]$, where $\U$ is a generalization of $\I$ to be more of an ~arbitrary shape.  
The typing rules are built on extensional [multimodal type theory](./multimodal-type-theory.md) which I have discussed elsewhere.



## TODO
To include
> This way, we are also rid of
the requirement that all internal operations commute with shape substitution; in fact, the
transpension generally does not (Section 2.1.7, [Nuy20b]).

Talk about the fresh weakening coquantifier and weakening

Talk about their categorical semantics more, pinning it down to more intuitive reasons why they chose an endofunctor multiplier (aka also what are non-cartesian variables), and talk about how it supports base categories that not objectwise pointable.

Obviously try to talk about intuition.