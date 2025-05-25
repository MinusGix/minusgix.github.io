+++
date = '2025-05-19T01:11:26-04:00'
draft = false
title = 'Introduction'
tags = ["Type Theory"]
categories = ["Type Theory"]
math = true
+++

Welcome to the All-of Type Theory.  

This is an attempt to explain important aspects of Type Theory as they become interesting to me, while also posing questions that I have.  
My focus will tend towards more practical considerations, especially those of software development.  

I will often link out to other works if I think they explain the topic better than I can.  

The core reason that I view it as important to provide these sorts of blog-posts is to spread a formal understanding of Type Theory further afield. In my opinion, many areas of the field lack good explanatory works. Both for those who haven't encountered the "new" but standard concepts such as sheaves, but also for those who have but don't want to spend quite a lot of time untangling a paper or concept themselves.

As well, I view the sheer amount of new concepts that strike at the reader when learning Type Theory (much like Category Theory) harms the ability to understand and get into any sort of flow of understanding a paper. Needing to search up a term is certainly necessary at times, but good pedagogy should try to make it clear what precisely an intuitive meaning of a statement is, and also try to be clear about definitions. This blog often adds reminders/notes throughout, whether ensuring you understand the term being utilized. Repeated reminders that don't distract, with simple explanations rather than the rather dense descriptions elsewhere (sorry nlab, I love you), help to ensure you learn the concept.

## Reading Order

While there isn't a set reading order, some topics implicitly assume some familiarity with other blogposts or type theory content I haven't even had the opportunity to write about yet!

Essentials:  
- [Introduction](../introduction)

Utility Concepts:
- [Locales](../../locales)
- [Sheaves](../sheaves)
- [Topoi](../topoi)

Intriguing Directions:
- [Multimodal Type Theory](../multimodal-type-theory): Add (non-substructural) modal operators to a Type Theory, only requiring the modality satisfy some basic properties to automatically get useful proofs of the Type Theory.
- [Transpension](../transpension): ...
- 

## Why this Focus?
I'm somewhat opinionated on my focus and what I think is important here. Skip this if you don't care.  

I *really* want a programming language that can prove theorems about general mathematics as well as about software written in it. I'd also love it to be low-level, because in my view a lot of important low-level software is often what really needs to be verified.  

Having a separate layer to prove properties has failed. There is excellent work done with these tools, but none of made their way into active programming usage outside of a few niche but important cases like aerospace software.  
There is also a lack of tooling which uses heuristics combined with formal verification to notice areas where software is likely to have bugs. If this existed in a good form, then it could be integrated into existing editors.  

The other alternative which commands much usage is that of functional programming languages. The most clear-cut case of being a Theorem Prover and Programming Language is Lean. Lean is a great language, it has improved the state of usability to a good degree, and probably helped kickstart Coq/Rocq into improving itself in that direction.  
Unfortunately, I don't think functional programming is going to catch on. While much has been written about the ability to optimize functional programming code, it has remained far weaker than ideal, and does not offer the capabilities to handle careful written performant code as you would in other languages. Functional programming has failed to become the mainstream paradigm of choice despite multiple decades.  

In my view, functional programming is an incidental consequence of being easier to reason about mathematically. An understandable motivation. However, there are strong reasons that much software is written in imperative languages.  
Lean has tried to address this with `do` notation and the like, but unfortunately it still suffers from a lack of usability. IO all over the place is also unpleasant.

Humans naturally think in terms of state that is modified. While certain expressions of this, such as OOP, have many flaws, the core idea is important.  
Even if you design your language to be functional under the hood, imperative needs to have strong support. This grows more important as we move down the stack.  

I expect this will be something that many disagree with, and that's fine. Much of my focus will be on focusing on various concepts in Type Theory which I think are useful to know in the hope that I can explain clearly.

## What is Type Theory?

Type Theory exists as an alternative to Set Theory. Intuitively, rather than sets, we have types.  

[What makes dependent type theory more suitable than set theory for proof assistants?](https://mathoverflow.net/questions/376839/what-makes-dependent-type-theory-more-suitable-than-set-theory-for-proof-assista) written by Andrej Bauer.  

As espoused above, a core problem with using Set Theory for a proof assistant is that it is simply too "untyped". Intuitively, as humans, we consider `{}` to be some random set, while you might have defined the natural number zero to be `{}` when doing a baseline construction of the set of natural numbers.  

My personal way of viewing this is that "true" set theory gives you two simple basic things:  
- A set contains atoms
- Atoms are just some names

This is a bit of a simplification, but it captures the core idea.  
You can formally define the natural numbers as a specific sort of set. $0 = \{\}$ and $1 = \{0\}$ and $2 = \{0, 1\}$ and so on.  
Write some functions like addition, and you can prove theorems about them.  

Why is this a problem?  

Well, for one, because it in a way gives us too many kinds of natural numbers.  
That specific definition of natural numbers? It's not the only one.  

We could have defined the natural numbers as simply $0 = \{\{\}}$ and then the same from then on.  

So, in reality, for all the theorems we would consider about the natural numbers, we're sortof having to parameterize them by a bunch of information about the specific *encoding* of the natural numbers.  

This is a bit of a pain.  

This sort of problem comes up if you decide to make some specific thing the lego out of which everything else is built.  
A prime example of this is that of binary digits in computer science. All we really have is some memory with a bunch of bits set to either 0 or 1. What your programming language does is have a specific *interpretation* of what those bits mean. Of what a specific region of memory encodes. It says "Oh, this region is an integer", and "this other region is a float". Despite them both having the same size, you call different functions on them.  
Just like in set theory, where you'd really have `add_1`, `add_2`, `add_3`, etc. for each encoding of the natural numbers.  

This can result in weird results where you say $1 = 2$ where the left-side is from a different encoding than the right-side.  

In practice, however, mathematicians do not pay attention to these details. They implicitly quantify over any encoding of the natural numbers with some properties.  
That's great!  

However, this is a problem for proof assistants which recognize that these "numbers" are made up of ~~bits~~ sets and can be broken down. You could of course add extra rules to your language that says that whenever it sees $ℕ$ it interprets the theorem as instead parameterized by an encoding with a particular set of rules.  

However, those set of rules and other tidbits? They're going to look a lot like Type Theory.  

Type Theory essentially does a move that you can see repeated a lot, of saying "Okay, but why not just take that as a primitive?"  
So, instead of things being made of sets, we have types declared as a collection of rules.  

```
type nat =
    | zero
    | succ nat
```
This encapsulates the basic conceptual idea of natural numbers.  
We can then write functions like addition and prove theorems about them.  


I'll note that this is still imperfect in a way, but it is in a form that I'm not sure there's much way to naturally avoid much further. We could design an alternative representation of Nat as finite binary strings which would have the same representation capacity.  

(Minor side note: Homotopy Type Theory manages some removal of extraneous representations with high inductive types, but that's a topic for another post.)


However, this methodology does still remove a lot of the painful duplication. It also avoids junk theorems which are more about the underlying encoding rather than the actual mathematics.  