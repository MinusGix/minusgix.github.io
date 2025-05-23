+++
date = '2025-05-19T01:32:50-04:00'
draft = true
title = 'Axiom of Choice'
math = true
+++

(Note: This document is even more of a hodgepodge of notes than usual without any sort of definite conclusion.)

## Introduction

The Axiom of Choice is an axiom often assumed in set theory. It is a statement about the ability to make choices from a set of options.

We will often shorten this to "**AC**".

### Formal Glance

Let $\mathcal{C}$ be some collection of non-empty sets.
Then, there exists a choice function $f$, such that: $$\forall A \in \mathcal{C}, f(A) \in A$$

That is, this function simply takes some arbitrary set and returns some element of that set.

### Intuition

This appears straightforward at first glance.  

Take some set, $A_0 = \{1, 2,3\}$, and we can define $f(A_0) = 1$.  
Rather trivial.  

We can even look at some larger sets, like the natural numbers. $\N = \{0, 1, 2, 3, \ldots\}$.  
We can define $f(\N) = 42$.  


Even for the real numbers, $\R$, we can define $f(\R) = 0$ just fine.  


So, really, this doesn't seem like that big of a deal. How is it different than any other axiom that adds something "obvious"?

Well that's what this article is about.



## The Bad Parts
There's a complexity to the statement of **AC** that is not immediately obvious. It applies even to sets for which you have no idea how to *name* the elements.  

For our finite sets, the natural numbers, and the real numbers, we can easily pick out a specific element for our definition of some choice function.  

But, what about:  
$$\mathcal{C} = \{A_\alpha \subset \R \mid \alpha \in I\}$$

where $I$ is some arbitrary uncountable index set.  

> [!Note]
> An "index set" is just a fancy way of saying a set of indices. Think of it like the usual $A_1, A_2, A_3, \ldots$ but not necessarily with any ordering, and it can be uncountable. If you want to be really specific, you can just think of any indexed set as a function $A : I \to \mathcal{C}$ where $A_\alpha = A(\alpha)$ and returns a specific element of $\mathcal{C}$ (which are sets themselves).  

This is a bit weird to say the least. We have some arbitrary subsets of the real numbers. And not only that, but we have an uncountable number of them!  

Now, for specific instances of this, we can actually define a choice function.  
Whatever setup we choose, the core idea would be to impose some *regularity* or *uniformity* on the sets $A_\alpha$. Some properties inherent to them that we can know apply, and can utilize to pick out a specific element.  
Like, an obvious one, is if we have that $\forall A \in \mathcal{C}, 0 \in A$ then we can simply define $f(A) = 0$ for any set $A$.  
This is an important observation that shows up not just with **AC**, that at times you need a certain sort of shared properties to be able to actually construct the values.


However, no such uniform construction exists in general.
If you are not given some nice properties about the sets within $\mathcal{C}$, then you can not actually define—whether by constructing it or specifying abstract rules for finding the function—a choice function.  

The Axiom of Choice, then, is effectively saying that this is not actually an issue. You do not need to be able to define a way to choose an element from each set, you can just *choose* one. You do not have to be able to do this even in *abstract principle* like much of mathematics has, you can simply pull a value.

### Non-Computability
The computer-science perspective is that your choice function is some sort of algorithm. Some sequence of steps that will take in some input, and return some output.  

This is a very physically grounded and natural perspective for thinking about mathematics. We do not necessarily require you to actually run the function when making a proof, but in principle, we would be able to and we are guaranteed that we can.

If you are able to construct a choice function, then that is equivalent to being able to specify steps to choose an element from any set in $\mathcal{C}$.  

However, if you have to rely on **AC**, then you are effectively going "I have a function with this property that you can not specify in a thousand thousand years, so I'm just going to assume it exists."  

Now, regardless of how grounded you think this is, it still breaks nice properties that mathematics could have. Computability provides nice properties for analyzing mathematics in a meta-sense, as well as letting us quite literally run math on computers in a way. It eliminates the correspondence between mathematical functions and algorithms.

That is, **AC** is a very non-physical axiom.

I consider this to be a sound reason for avoiding assuming it for Type Theory and for mathematics as merged with programming languages.

### Banach-Tarski Paradox

> A solid ball in 3-dimensional space can be split into a finite number of non-overlapping pieces, which can then be reassembled (using only rotations and translations) into two solid balls of the same size as the original.

The Banach-Tarski Paradox is a theorem that shows that you can take a sphere, and by applying **AC** paired with the Measure Theory rules, you can partition the sphere into five pieces, and then rearrange those pieces to form two spheres of the same size as the original.  

This clearly contradicts our intuition. How could you double the volume of a sphere?!

What gets even weirder is that it depends on the Axiom of Choice. You can not actually construct these exotic parts-of-the-sphere without it. ~~They're eldritch creatures, these parts-of-the-sphere.~~
Another interesting point is that these parts-of-the-sphere are actually not actually measurable. You can not assign a nice value to their "volume" in the way that we usually do.

For many, this seems like a rather strong reason to avoid **AC**. It collides with standard intuition rather extremely. Why can we break a sphere into two spheres with the same volume??

I do think this does provide evidence against **AC**, but that it is somewhat less strong than it sounds.  

#### Whether $\R$ models reality
A lot of our intuitions for finite mathematics is based around reality. In reality it seems quite clear that there's no way for us to break apart a sphere like this.  
However, euclidean space has always been an approximation of physical reality. Even for classical physics, $\R^3$ being so smooth and continuous is an approximation of a space made up out of discrete atoms. A good approximation, and in a way you can think of it as the "limit" of the discrete space where atoms get arbitrarily small and planck lengths go to zero. However, we should expect it to falter somewhere, somewhen.  
In classical physics, Zeno's paradoxes don't... really apply. You can either have a movement function that is continuous with respect to time, rather than discrete, or you can simply say that the space really is discrete.  

This answer then, is that $\R^3$ simply behaves in a weird manner. It has its rules, and it is more your fault for believing your approximation was the truth of things.

----

This evaluation does hold up in my opinion.  
However, I do think those that believe it should take it as further evidence against $\R$ as a central object of study. It has nice properties, but negative properties like this should make one take it suspect as a basis for your reasoning. (Why not work with $\Q$? Or an abstract algebraic structure?)

I do still think it is surprising even so.

#### Wildness
In a way these pieces you choose are very "wild". They have an obscene amount of complexity specifying them, which is why you can't just construct them directly. The best metaphor I like dragging out is that of a fractal—but not one with a neat predictable self-similarity. Just infinite depth, every turn a surprise.  
I tend to call this sort of thing "intricately complex". You're splitting things up in a very unnatural way, with countably infinite choices over countably infinite sets such that you need a powerful axiom to even say that they *exist*.

#### Conception of Space

> There are two ingredients in the Banach-Tarski decomposition theorem:
>
> - The notion of space, together with derived notions of part and decomposition.
> - The axiom of choice.
>
> Most discussion about the theorem revolve around the axiom of choice. I would like to point out that the notion of space can be put under scrutiny as well.
>
> The Banach-Tarski decomposition of the sphere produces non-measurable parts of the sphere. If we restrict the notion of "part" to "measurable subset" the theorem disappears. For instance, if we move over into a model of set theory (without choice) in which all sets are measurable, we will have no Banach-Tarski. This is all well known.
>
> Somewhat amazingly, we can make the Banach-Tarski decomposition go away by extending the notion of subspace, and keep choice too. Alex Simpson in [Measure, Randomness and Sublocales](https://web.archive.org/web/20160909042100/http://homepages.inf.ed.ac.uk/als/Research/Sources/mrs.pdf) (Annals of Pure and Applied Logic, 163(11), pp. 1642-1659, 2012) shows that this is achieved by generalizing the notion of topological space to that of locale. He explains it thus:
>
> > "The different pieces in the partitions defined by Vitali and by Banach and Tarski are deeply intertangled with each other. According to our notion of “part”, two such intertangled pieces are not disjoint from each other, so additivity does not apply. An intuitive explanation for the failure of disjointness is that, although two such pieces share no point in common, they nevertheless overlap on the topological “glue” that bonds neighbouring points in $\R^n$
> > together."
>
> Peter Johnstone explained in [The point of pointless topology](http://pointlesstopology.com/the-point-of-pointless-topology.pdf) why locales have mathematical significance that goes far beyond fixing a strange theorem about decomposition of the sphere. Why isn't everyone using locales? I do not know, I think it is purely a historic accident. At some point in the 20th century mathematicians collectively lost the idea that there is more to space than just its points.
>
> I personally prefer to blame the trouble on the notion of space, rather than the axiom of choice. As far as possible, geometric problems should be the business of geometry, not logic or set theory. Mathematicians are used to operating with various kinds of spaces (in geometry, in analysis, in topology, in algebraic geometry, in computation, etc.) and so it seems only natural that one should worry about using the correct notion of space first, and about underlying foundational principles later. Good math is immune to changes in foundations.
> - **Andrej Bauer** on [Axiom of Choice Banach Tarski and Reality](https://mathoverflow.net/q/260072)

This is a solution that I find appealing and interesting.

[Locales](locales) have some nice properties that work better constructively. They provide a stronger logical foundation as they to some degree include the logical rules in their structure, whereas normal topological spaces collapse that—only really considering points to exist.

### Zorn's Lemma
[Zorn's lemma in nLab](https://ncatlab.org/nlab/show/Zorn%27s+lemma)

> The Axiom of Choice is obviously true; the Well Ordering Principle is obviously false; and who can tell about Zorn's Lemma?


Zorn's "Lemma" is equivalent to the Axiom of Choice (as well as the Well-Ordering Principle).  

Formal:
> $P$ is a partially ordered set where every chain (totally ordered subset) has an upper bound that lies within $P$.
>
> Then, $P$ has at least one maximal element. An element $m \in P$ such that $\lnot\exist x \in P, m < x$

That is, if every "clearly ordered" parts of $P$ (the chains) have their ceiling within $P$, then there is some element that is the largest element in the entirety of $P$.  

Like with other cases of Choice, there's specific instances of this where you can simply have a construction of the set that lets you easily prove a special-case of this lemma.  

(TODO: is this remotely right?)
One conception of looking at this is that just because you have all these chains that have an upper bound, you're merely "pushing against" a possible maximal element. All of the chains you have might not be enough to specify it in general, and so properly picking it out requires some sort of choice.  
Each chain sortof probes the structure and hints at something, but without the Axiom of Choice you can't necessarily pin it down as actually existing—or pinning it down to a specific variant if there are multiple values that satisfy.

### Well-Ordering Theorem
Formal:
> For any set $S$, there is some well-ordering $\leq$ on $S$

For cases like finite sets or some infinite sets like the natural numbers, this is rather trivial.  

But, when applied to the real numbers it becomes... odd.

Let's look back at the definition of a well-ordering.  
> - Total linear order
>   - For all $a,b \in S, a \lt b \lor a =b \lor b \lt a$
> - Transitive: $a \lt b \land b \lt c \implies a \lt c$
> - Antisymmetric: $a \le b \land b \le a \implies a = b$
> - Well-founded: Every non-empty subset of $S$ has a *least element* by $\le$

The first three are intuitive and you could handle them on the real numbers without issue.  

But, what about well-foundedness?

Part of the reason this is sometimes said to be false is because people think of the *canonical* ordering of the reals.  
There, we can find a counter-example: $(0, 1]$ has no least element. $0.1$? We can find a smaller value of $0.01$. $0.001$? We can find a smaller value of $0.0001$. Etc.

However, it is important to note that the well-ordering principle is simply saying that there is "some" well-ordering of the set. A set can have whatever orderings you like.  


However, before we clap ourselves on the back that we've solved the confusion, continue thinking about this well-ordering that it says exists on the real numbers.  
It means that $(0, 1]$ has some least value. Okay? So what? Perhaps it defines $0.1$ as the least value. Weird but legal.

The problem being that we can't actually define this well-ordering. It is obscenely intricately complex in how it works, turning on a dime on infinitely detailed conditions. This well-ordering is also not continuous.

----

If someone says that we can suppose an ordering of a set, this is likely what they're referring to.  
If we connect this back to a computational perspective, this is saying that if we want to "investigate" a set, there's always some privileged order that we can put on it. To me that's not so unreasonable but at the same time seeming like a strong statement, pulling a very complex procedure from nowhere.

## Different kinds of Choice
There's a variation of this that provides an argument against the typical form of the Axiom of Choice, but yet still allows you to use Choice in many cases.  

The simple answer is that there's multiple ways to decide "what things" you can choose from. The typical formulation is that of uncountable choice: where you can choose an element from an uncountable set.  
However, there's also countable choice, which is the ability to choose an element from a countable set.
Or, dependent choice where you can choose an element based on a previous choice. Effectively a sequence of choices.  

Both of these are weaker than the full axiom of choice. But they allow you to prove many of the theorems you might want to utilize.

> It's notable that most of the "bread and butter" mathematical consequences of the axiom of choice are actually consequences of countable choice. (Every infinite set contains a countable subset, a countable union of countable sets is countable, etc.) The Hahn-Banach theorem is a counterexample, but only if you want it for nonseparable spaces, and I can't think of any time I've ever needed this. When restricted to separable Banach spaces it doesn't require any choice principle at all! Whereas the seemingly pathological consequences of choice (existence of nonmeasurable sets, Banach-Tarski, well-ordering of the real line) generally do not follow from countable choice.
>
> So the argument from mathematical value seems to me to support countable choice more than full choice. But that isn't a very strong argument, is it? We can't decide whether an axiom is true based on whether we like its consequences. At best it's suggestive.
>
> Incidentally, I had the impression when I read Zermelo that he had great polemical skill, but none of his arguments seemed to get directly to the truth of the axiom. He argues for the mathematical value of the axiom. He points out that his critics have themselves on occasion unwittingly used the axiom, which is a devastating point, but has little bearing on the question of truth. (If I'm not mistaken, those unwitting uses were all of countable choice, by the way.)
>
> You ask if one should "believe" the axiom of choice, and I think you are right to put the word "believe" in quotes. I feel strongly that set-theoretic assertions are objectively meaningful, but I also feel that philosophers of mathematics have done a very poor job of clarifying what sets are. (Halmos: "A pack of wolves, a bunch of grapes, or a flock of pigeons are all examples of sets of things." Black: "It ought then to make sense, at least sometimes, to speak of being pursued by a set, or eating a set, or putting a set to flight.") If we can't even get that straight, it's hard to come to grips with questions about the truth of questionable axioms.
> - **Nik Weaver** on [Axiom of Choice Banach Tarski and Reality](https://mathoverflow.net/questions/260057/axiom-of-choice-banach-tarski-and-reality/260065#260065)

Nik Weaver's argument is that if you are using the reason of utility behind **AC** then you should only assume countable choice. Uncountable choice has less utility and has weird exotica like the Banach-Tarski paradox, so you should at the least be cautious about necessarily utilizing it.

## Practical
TODO: remarks about proofs that need different versions of choice. But also mention constructive versions that do not need choice, but might be weaker, or are actually more meaningful.

## Random Thoughts
### Wrapped Choice
Like how in provability logic we might have $\box P$ behave somewhat differently than literally having $P$, should we consider having such a symbol for choice? Have so that acquiring $a \in A$ is distinct from $(\box a) \in A$? That is, it behaves differently and perhaps has some restricted rules to make the surrounding system behave better.


This seems clearly related to propositional truncation.  
It lets us convert forwards, $a : A \mapsto |a| : ||A||$ but not backwards.  

To use some $x : ||A||$, you must map into a proposition.  
$P : ||A|| \to Prop$ (a proposition about elements of $A$)  
$\forall a : A, P(|a|) \implies \forall x : ||A||, P(x)$  
That is, if for all the actual elements of $A$ you can prove $P$ for the truncated value, then you can prove $P$ for the truncated set overall.
Essentially, you can only reason about the chosen element in a way which is insensitive to which element was chosen. $|a|$ is effectively throwing away all the identity information about $a$, you just know it is some element of $A$ and whatever properties you can prove about elements of $A$ will hold for $|a|$.

So, $x \in ||A||$ is "some choice has been made". This may even be as simply as $||A|| = \{\star\}$ and $x = \star$, having no identifying information about how $x$ links back to any specific element of $A$.   
  
You can then do Hilbert's $\epsilon$-operator, $\epsilon_A : ||A|| \to A$ to go backwards, effectively the axiom of choice.  
Notice that if you do have uniqueness, that is effectively that $||A|| = \{\star\}$, then the operator just gives you some element of $A$. But that's just the axiom of choice as usual, you aren't going *fully* backwards.

