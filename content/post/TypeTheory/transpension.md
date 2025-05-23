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

This paper came to my interest due to the mention in the slides linked above of using [MTT](./MultimodalTypeTheory.md) (Multimodal Type Theory) for 'variance', and MTras (Modal Transpension System for substructural intervals.  
I like substructurality. I think it makes a type theory much nicer as a programming language, allowing us to model things as "fundamentally" substructural.


So, we'll take a look at Transpension, and see precisely what it gives us as a tool to work with. The paper is nontrivial to understand.  

The first way to look at it is that it takes multiple existing special-cases of cool features that have been discussed in Type Theory literature, and provides a general tool to specialize them.

----

