+++
date = '2025-05-19T02:00:01-04:00'
draft = true
title = 'Infinity'
+++

## Introduction

## Predicativism
TODO

## Constructivism
TODO

## Continuum Hypothesis
Effectively the Continuum Hypothesis collapses the space between $\aleph_0$ and $\aleph_1$ into nothingness. (Effectively, that $2^\aleph_0 = \aleph_1$)

I've long considered this at least somewhat suspect. Why should concepts of infinity necessarily be linearly ordered? Why can there not effectively be a tree of distinct kinds of infinities with odd properties at the edges?


But, that we can not neatly name these different sorts of infinities? That we do not have any sort of intuitive grasp on distinctions between them that we might for countable vs uncountable?   
That lack of clarity makes me suspicious of assuming $\lnot \text{CH}$. As far as I know we do not get an interesting (but reasonably definable) splitting of 'infinite' like we do the concept of 'finite' in constructive mathematics. That overall makes me suspect of assuming $\lnot \text{CH}$.


As well, with **CH**, sets of real numbers behave better.

As well, assuming not-**CH** seems a bit weaker than we'd like. Probably because it is simply saying that some very specific kind of neatness about infinity is not true. That still leaves substantial indeterminancy about the nature of infinity.

> The lesson of much of this analysis is that many of the most natural open questions turn out to be themselvesd independent of ZFC, even when one wants ¬CH. For example, the question of whether all sets that are intermediate in size between the natural numbers and the continuum should be Lebesgue measure 0, is independent of ZFC+¬CH. The question of whether only the countable sets have continuum many subsets is independent of ZFC+¬CH.
> ...
> Nevertheless, there is a growing body of research on some sophisticated axioms in set theory called forcing axioms, which have powerful consequences, and many of these new axioms imply the failure of CH. 
[In set theories where Continuum Hypothesis is false, what are the new sets?](https://mathoverflow.net/questions/10227/in-set-theories-where-continuum-hypothesis-is-false-what-are-the-new-sets)

## Axiom of Determinacy
(TODO: more explanation)

Effectivelly assumes that some infinite games are determined.  

AD can be used to prove that every set of reals is either countable, or has the same countability as $\R$.

This results in nice properties like every set of reals being Lebesgue measurable. As well, it results in that every set of reals is either countable or of size continuum. 

Note that this still allows there to be other cardinalities between $|\N| = \aleph_0$ and $|\R| = 2^{\aleph_0}$, we do not necessarily have that $\aleph_1 = 2^{\aleph_0}$.  

So it makes the reals more well-behaved, but leaves open vagaries. It does make one more suspicious of $\text{CH}$—why can we not, even in principle, make subsets that are infinite in some distinct sense? Is there some way to reason about these odd sets?

However, $\text{AD}$ precludes the full axiom of choice.

$\text{AD}$ is also inconsistent with $\text{CH}$ in the presence of large cardinals.

I'd be interested in whether there's versions of this which have a computational interpretation.

## Generally
However, one perspective I've played with is that part of our whole issues with infinity is that we simply do not pin down what we mean by infinity and the methodology of handling it. This is why CH and AC are independent of ZF, because we do not pin down the meaning of infinity enough with baseline axioms and so you need them to get somewhere.

However, this does encourage differing perspectives. Trying to find weaker and simpler axioms, especially those ostensibly about finite or countable objects and seeing how those affect the behavior of infinite objects. I'm not sure **CH** is the right "level" of axiom to be looking at, though I do think **AC** is not a terrible choice to consider.


But, one can take this further. That the core issue with infinity is that while finite objects have reasonably well-behaved properties that also often(ish) transfer between different considerations, that they are thus more "solid" and "real". Countable objects as well, though I have considered that you should instead consider countable objects that are required to be defined in a nice way.

So you can take this both ways. That we really need new axioms to pin down infinity. Or, instead, that we should remain ambiguous about the nature of infinity as much as possible due to a lack of grounding.