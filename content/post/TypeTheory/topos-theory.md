+++
date = '2025-06-02T10:00:00-00:00'
draft = true
title = 'Topos Theory: A Categorical Foundation for Mathematics and Logic'
tags = ["Type Theory", "Category Theory", "Logic"]
categories = ["Type Theory"]
math = true
+++

**Topic**: An introduction to topos theory, its fundamental concepts, and connections to type theory and mathematics.

**Abstract**:
> Topos theory provides a unified categorical framework for understanding logic, set theory, and geometry. A topos is a category that behaves like the category of sets but with an internal logic that can vary dramatically. This post introduces the core concepts of topos theory—from elementary topoi and subobject classifiers to geometric morphisms and the internal language. We explore how topoi serve as models for intuitionistic type theory, generalize classical mathematics, and provide foundations for synthetic differential geometry, homotopy type theory, and more.

## Introduction

Imagine a mathematical universe where the law of excluded middle might not hold, where functions can know about their computational history, or where infinitesimals exist as first-class citizens. These are not fantasies but concrete mathematical structures studied in topos theory.

Topos theory emerged in the 1960s from Grothendieck's revolutionary work in algebraic geometry and Lawvere's categorical foundations for mathematics. What started as an abstraction of sheaf theory has grown into a fundamental framework that:

- Unifies diverse areas of mathematics under a single categorical umbrella
- Provides semantics for constructive and intuitionistic logic
- Models computational phenomena in type theory
- Generalizes set theory while remaining remarkably concrete

This post will guide you through topos theory with escalating complexity, starting from basic categorical concepts and building to sophisticated applications in type theory and mathematics.


## Categories: A Quick Refresher

Before diving into topoi, let's establish our categorical foundation. A **category** $\mathcal{C}$ consists of:
- Objects: $A, B, C, \ldots$
- Morphisms (arrows): $f: A \to B$
- Composition: $(g \circ f): A \to C$ for $f: A \to B$, $g: B \to C$
- Identity morphisms: $\text{id}_A: A \to A$

With axioms ensuring associativity of composition and identity laws.

The category $\mathbf{Set}$ of sets and functions serves as our prototypical example. But categories appear everywhere: groups (one object), posets (at most one arrow between objects), and topological spaces with continuous maps.

## Elementary Topoi: The Basics

An **elementary topos** is a category that shares the essential features of $\mathbf{Set}$ while allowing for radically different internal logic.

> [!note]
> **Definition (Elementary Topos):**
> A category $\mathcal{E}$ is an elementary topos if it has:
> 1. Finite limits (including a terminal object $1$)
> 2. Exponentials (function objects $B^A$ for all objects $A, B$)
> 3. A subobject classifier $\Omega$

Let's unpack this definition piece by piece.

### Finite Limits

Finite limits generalize constructions like products and equalizers. The **terminal object** $1$ is the categorical analogue of a one-element set—there's exactly one arrow $A \to 1$ from any object $A$.

Products $A \times B$ come with projections $\pi_1: A \times B \to A$ and $\pi_2: A \times B \to B$ satisfying the expected universal property. In $\mathbf{Set}$, this is just the Cartesian product.

### Exponentials

The **exponential object** $B^A$ represents the "object of all morphisms from $A$ to $B$". It comes with an evaluation map:
$$\text{ev}: B^A \times A \to B$$

In $\mathbf{Set}$, $B^A$ is the set of all functions from $A$ to $B$. The existence of exponentials means our topos is **cartesian closed**—a crucial property for interpreting typed lambda calculus.

### The Subobject Classifier

This is where topoi become magical. A **subobject classifier** is an object $\Omega$ with a morphism $\text{true}: 1 \to \Omega$ such that for every monomorphism (injective map) $m: S \hookrightarrow A$, there exists a unique **characteristic map** $\chi_m: A \to \Omega$ making this square a pullback:

```
S -----> 1
|        |
m|        |true
v        v
A -----> Ω
   χ_m
```

In $\mathbf{Set}$, $\Omega = \{0, 1\}$ with $\text{true}(∗) = 1$. The characteristic map $\chi_m$ sends elements in the image of $m$ to $1$ and others to $0$.

> [!tip]
> **Intuition**: The subobject classifier $\Omega$ is the "object of truth values" in our topos. Each element of $\Omega$ represents a possible truth value, and $\text{true}$ picks out the designated "true" value.

## Internal Logic: Where Things Get Interesting

The subobject classifier transforms our topos into a universe with its own internal logic. For each object $A$, the subobjects $\text{Sub}(A)$ form a Heyting algebra—the algebraic structure of intuitionistic logic.

### Heyting Algebras: The Structure of Intuitionistic Logic

A **Heyting algebra** is a bounded lattice with an implication operation satisfying:
$$c \leq (a \Rightarrow b) \text{ if and only if } c \wedge a \leq b$$

This captures the essence of intuitionistic logic where proving $a \Rightarrow b$ means constructing a method to transform any proof of $a$ into a proof of $b$.

> [!note]
> **Key Difference from Boolean Algebras**: 
> In a Boolean algebra, we have $\neg\neg p = p$ (double negation elimination). In a Heyting algebra, we only have $p \leq \neg\neg p$. The converse requires the law of excluded middle!

### Logical Operations in Detail

Given subobjects $S, T \hookrightarrow A$ with characteristic maps $\chi_S, \chi_T: A \to \Omega$, we can define:

#### Conjunction (Meet)
The intersection $S \cap T$ is computed as the pullback:
```
S ∩ T -----> T
  |           |
  |           |
  v           v
  S -------> A
```
Its characteristic map $\chi_{S \cap T}$ is given by the unique map making the diagram commute with the product $\Omega \times \Omega$.

#### Disjunction (Join)  
The union $S \cup T$ is the image of the coproduct map $[i_S, i_T]: S + T \to A$. In the internal logic, this corresponds to "there exists a proof of $S$ or a proof of $T$"—constructively different from classical disjunction!

#### Implication
The most subtle operation. For $S \Rightarrow T$, we form the equalizer:
```
S ⇒ T -----> A
  |           |
  |           |ev
  v           v
  1 -------> Ω^Ω
```
where the bottom map classifies the largest subobject of $\Omega$ contained in the image of $\chi_S \Rightarrow \chi_T$.

#### Negation
Negation is implication into the initial object: $\neg S = (S \Rightarrow \bot)$ where $\bot$ is the empty subobject. Crucially:
- $S \subseteq \neg\neg S$ always holds
- $\neg\neg S \subseteq S$ requires classical logic

> [!example]
> **Computing in Presheaves**: In $\mathbf{Set}^{\mathcal{C}^{\text{op}}}$, for presheaves $F, G$ and subfunctors $S \subseteq F$, $T \subseteq G$:
> - $(S \cap T)(c) = S(c) \cap T(c)$ (pointwise)
> - $(S \cup T)(c) = S(c) \cup T(c)$ (pointwise)
> - $(S \Rightarrow T)(c) = \{x \in F(c) : \forall f: d \to c, F(f)(x) \in S(d) \implies F(f)(x) \in T(d)\}$
>
> Notice how implication becomes "hereditary": it must hold at all future stages!

### Truth Values Beyond True/False

The subobject classifier $\Omega$ can be remarkably rich:

#### In Sheaf Topoi $\text{Sh}(X)$
Truth values are **open sets** of $X$. For a sheaf $F$ and subsheaf $S \subseteq F$:
- The characteristic map $\chi_S: F \to \Omega$ sends a section $s \in F(U)$ to the largest open $V \subseteq U$ where $s|_V \in S(V)$
- Logical operations are: $U \wedge V = U \cap V$, $U \vee V = U \cup V$, $U \Rightarrow V = \text{int}(U^c \cup V)$
- Double negation: $\neg\neg U = \text{int}(\overline{U})$ (interior of closure)

> [!tip]
> **Geometric Intuition**: A proposition is "true on an open set" rather than absolutely true. This models situations where truth is local or contextual.

#### In Presheaf Topoi $\mathbf{Set}^{\mathcal{C}^{\text{op}}}$
Truth values form the presheaf of **sieves** (downward-closed sets of morphisms). At each stage $c \in \mathcal{C}$:
- $\Omega(c) = \{S \subseteq \mathcal{C}/c : S \text{ is a sieve}\}$
- A sieve represents "ways of knowing" something is true
- Kripke semantics: propositions can become true over time but never false

#### In the Effective Topos $\mathcal{E}\text{ff}$
Truth values correspond to **recursively enumerable sets** modulo recursive equivalence:
- Classical truth ($\top$) = any r.e. set containing a number
- Classical falsity ($\bot$) = the empty set
- Many intermediate truth values representing degrees of computability
- $\neg\neg\top \neq \top$ in general (not all truths are computably verifiable)

### The Failure of Classical Logic

Let's see concretely why excluded middle fails:

> [!example]
> **In $\text{Sh}(\mathbb{R})$**: Consider the subsheaf of constant functions $\mathbb{R} \to \mathbb{R}$. Let $P$ be "the function is zero". Then:
> - $P$ is true on $\{0\}$
> - $\neg P$ is true on $\mathbb{R} \setminus \{0\}$  
> - $P \vee \neg P$ is true on $\{0\} \cup (\mathbb{R} \setminus \{0\}) = \mathbb{R}$
> - But this equals $\top$ only if $\{0\}$ and $\mathbb{R} \setminus \{0\}$ cover $\mathbb{R}$ **as open sets**, which they don't!

### Modalities and Intermediate Logics

Many topoi support **modalities**—operations on $\Omega$ that modify propositions:

1. **Double Negation**: $\neg\neg: \Omega \to \Omega$ (Lawvere-Tierney topology)
   - Makes the topos "more classical"
   - In sheaves: $\neg\neg U = \text{int}(\overline{U})$ (regularization)

2. **Dense/Closed Modalities**: In spatial topoi
   - $\square P$ = "$P$ is dense" (true on a dense open)
   - $\lozenge P$ = "$P$ is somewhere true" (support is non-empty)

3. **Temporal Modalities**: In presheaf topoi over posets
   - $\square P$ = "$P$ is always true in the future"
   - $\lozenge P$ = "$P$ is eventually true"

> [!note]
> **Lawvere-Tierney Topologies**: A topology $j: \Omega \to \Omega$ on a topos satisfies:
> - $j \circ \text{true} = \text{true}$ (truth is dense)
> - $j \circ j = j$ (idempotent)
> - $j$ preserves finite meets
>
> Each topology gives a "notion of density" and induces a subterminal object of sheaves.

### Computing with Internal Logic

When working internally, these logical differences have computational consequences:

```
-- In classical logic (Set):
excludedMiddle : (P : Prop) → P ∨ ¬P
excludedMiddle P = magic  -- We can't construct this!

-- In a sheaf topos Sh(X):
-- P ∨ ¬P only when P corresponds to a clopen set

-- In presheaves:
-- P ∨ ¬P only when P is "decided at each stage"
```

The internal logic forces us to work constructively, which often leads to stronger, more informative proofs.

## Examples: Building Intuition

### Example 1: The Category of Sets

$\mathbf{Set}$ is the primordial topos where:
- $\Omega = \{0, 1\}$ 
- Logic is classical (Boolean)
- Every object is "discrete" with no additional structure

### Example 2: Presheaf Topoi $\mathbf{Set}^{\mathcal{C}^{\text{op}}}$

For a small category $\mathcal{C}$, the functor category $\mathbf{Set}^{\mathcal{C}^{\text{op}}}$ (presheaves on $\mathcal{C}$) is always a topos.

> [!example]
> **Kripke Models**: Let $\mathcal{C}$ be a poset of "possible worlds". A presheaf assigns to each world a set of "facts true at that world". The subobject classifier tracks "eventually true" propositions.

### Example 3: Sheaves on a Topological Space

For a topological space $X$, the category $\text{Sh}(X)$ of sheaves is a topos where:
- Objects are "continuously varying sets" over $X$
- $\Omega$ is the sheaf of open sets
- Logic is intuitionistic and "spatial"

> [!note]
> **Gluing**: In sheaf topoi, we can glue local data that agrees on overlaps—a fundamental principle in geometry and physics.

## Geometric Morphisms: Maps Between Universes

A **geometric morphism** $f: \mathcal{F} \to \mathcal{E}$ between topoi consists of a pair of functors forming a special kind of adjunction.

> [!note]
> **Definition**: A geometric morphism $f: \mathcal{F} \to \mathcal{E}$ is an adjoint pair $(f^*, f_*)$ where:
> - $f^*: \mathcal{E} \to \mathcal{F}$ is the **inverse image** functor
> - $f_*: \mathcal{F} \to \mathcal{E}$ is the **direct image** functor
> - $f^* \dashv f_*$ (left adjoint to right adjoint)
> - $f^*$ preserves finite limits (in particular, the terminal object)

### Understanding the Adjunction

The adjunction $f^* \dashv f_*$ means we have a natural bijection:
$$\text{Hom}_{\mathcal{F}}(f^*(E), F) \cong \text{Hom}_{\mathcal{E}}(E, f_*(F))$$

This captures the idea that pulling back and pushing forward are dual operations.

> [!example]
> **Continuous Maps Induce Geometric Morphisms**: 
> For a continuous map $g: Y \to X$ between spaces, we get a geometric morphism $\text{Sh}(g): \text{Sh}(Y) \to \text{Sh}(X)$:
> - $g^*(\mathcal{F})(V) = \mathcal{F}(g(V))$ for open $V \subseteq Y$ (pullback sheaf)
> - $g_*(\mathcal{G})(U) = \mathcal{G}(g^{-1}(U))$ for open $U \subseteq X$ (pushforward sheaf)
>
> The adjunction captures: sections over $g(V)$ correspond to sections over $V$ pushed forward.

### Essential Geometric Morphisms

A geometric morphism $f$ is **essential** if $f^*$ has a further left adjoint $f_!$:
$$f_! \dashv f^* \dashv f_*$$

> [!tip]
> **Local Homeomorphisms**: Essential geometric morphisms correspond to local homeomorphisms in topology. The extra adjoint $f_!$ extends sections by zero outside their support.

### Surjective and Injective Geometric Morphisms

Geometric morphisms have a factorization system:

1. **Surjection**: $f$ is surjective if $f_*$ is faithful
   - Corresponds to surjective maps in topology
   - Examples: $\text{Sh}(X) \to \text{Sh}(Y)$ from a surjective continuous map

2. **Inclusion**: $f$ is an inclusion if $f^*$ is full and faithful
   - Corresponds to subspace inclusions
   - Gives a "subtopos" $\mathcal{F} \subseteq \mathcal{E}$

Every geometric morphism factors as:
$$\mathcal{F} \xrightarrow{\text{surjection}} \mathcal{G} \xrightarrow{\text{inclusion}} \mathcal{E}$$

### Points: Windows into a Topos

A **point** of a topos $\mathcal{E}$ is a geometric morphism $p: \mathbf{Set} \to \mathcal{E}$.

> [!note]
> **Stalk Functor**: For a point $p$, the inverse image $p^*: \mathcal{E} \to \mathbf{Set}$ is called the **stalk functor** at $p$. It evaluates objects "at the point".

#### Examples of Points

1. **Points of $\mathbf{Set}$**: Only the identity morphism

2. **Points of $\text{Sh}(X)$**: For each $x \in X$, we have a point $p_x: \mathbf{Set} \to \text{Sh}(X)$
   - $p_x^*(\mathcal{F}) = \mathcal{F}_x$ (the stalk at $x$)
   - $p_{x*}(S)$ is the skyscraper sheaf at $x$ with fiber $S$

3. **Points of $\mathbf{Set}^{\mathcal{C}^{\text{op}}}$**: For each $c \in \mathcal{C}$, evaluation at $c$ gives a point
   - $\text{ev}_c^*(F) = F(c)$
   - $\text{ev}_{c*}(S) = \mathcal{C}(-, c) \times S$ (representable presheaf times $S$)

4. **Points of $[G, \mathbf{Set}]$** (G-sets for a group $G$): Fixed points of the $G$-action
   - Each corresponds to a group homomorphism $G \to 1$

### Pointless Topoi

Some topoi have **no points** at all! Examples include:

1. **Double Negation Sheaves**: The topos of sheaves for the double negation topology on a Boolean algebra
2. **Synthetic Differential Geometry**: Models with infinitesimals have no Set-valued points
3. **Certain Quotient Topoi**: Like the "bad quotient" $\mathbb{R}/\mathbb{Q}$ as a topos

> [!warning]
> **Deligne's Theorem**: A coherent topos has enough points if and only if it satisfies a strong completeness theorem for its internal logic. Pointless topoi can still have rich internal structure!

### Morphisms Between Presheaf Topoi

For small categories $\mathcal{C}, \mathcal{D}$, geometric morphisms $\mathbf{Set}^{\mathcal{C}^{\text{op}}} \to \mathbf{Set}^{\mathcal{D}^{\text{op}}}$ correspond to:
- Functors $F: \mathcal{C} \to \mathcal{D}$ (going the "opposite" direction!)
- More generally, profunctors $\mathcal{D} \not\to \mathcal{C}$

> [!example]
> **Restriction and Extension**: For a functor $F: \mathcal{C} \to \mathcal{D}$:
> - $F^*: \mathbf{Set}^{\mathcal{D}^{\text{op}}} \to \mathbf{Set}^{\mathcal{C}^{\text{op}}}$ is restriction along $F$
> - $F_*$ is right Kan extension along $F$
> - If $F$ is full and faithful, we get an inclusion of topoi

### Base Change and Dependent Types

Geometric morphisms interact beautifully with slice topoi. For $f: \mathcal{F} \to \mathcal{E}$ and $E \in \mathcal{E}$:

```
\mathcal{F}/f^*(E) -----> \mathcal{F}
       |                    |
       |                    |f
       v                    v
\mathcal{E}/E ----------> \mathcal{E}
```

This square commutes up to equivalence, capturing how dependent types transform under geometric morphisms.

### Logical Morphisms

A geometric morphism $f$ is **logical** if $f^*$ also preserves the subobject classifier:
- $f^*(\Omega_{\mathcal{E}}) \cong \Omega_{\mathcal{F}}$
- Preserves all first-order logic
- Rare but important (e.g., between Boolean topoi)

### Computing Inverse Images

Given a geometric morphism $f: \mathcal{F} \to \mathcal{E}$, computing $f^*$ often involves:

1. **For sheaf topoi**: Pullback of sheaves along continuous maps
2. **For presheaf topoi**: Restriction along functors  
3. **For slice topoi**: Pullback along morphisms
4. **For classifying topoi**: Interpreting the theory in a new model

> [!tip]
> **Practical Computation**: To find $f^*(E)$, look for the "most general" object in $\mathcal{F}$ that maps to $E$ under $f_*$. The adjunction often determines it uniquely.

## The Internal Language: Types and Logic United

Every topos has an **internal language**—a type theory that describes its objects and morphisms. This creates a profound connection between:
- Category theory (topoi)
- Logic (intuitionistic/constructive)
- Type theory (dependent types)

### Types as Objects

In the internal language:
- Objects become types: $A, B, C, \ldots$
- Morphisms become terms: $t: A \vdash f(t): B$
- The terminal object is the unit type: $1$
- Products are product types: $A \times B$
- Exponentials are function types: $A \to B$

### Propositions as Subobjects

The crucial insight: **propositions are subobjects of the terminal object**. 

For a proposition $P$, we have:
- $P: 1 \to \Omega$ (a truth value)
- Proofs of $P$ are elements of the corresponding subobject
- Logical operations translate to lattice operations on $\text{Sub}(1)$

> [!note]
> **Curry-Howard Extended**: The internal language extends Curry-Howard correspondence to a full dependent type theory with:
> - Dependent types via pullbacks
> - Existential types via images
> - Identity types (in some topoi)

### Working Internally

When reasoning "inside" a topos, we adopt its internal viewpoint, which can differ dramatically from classical set theory.

> [!example]
> **Internal vs External**: 
> - **External**: "The sheaf $\mathcal{F}$ has a global section"
> - **Internal**: "There exists $s: 1 \to \mathcal{F}$"
> 
> These aren't always equivalent! In $\text{Sh}(X)$, internal existence means "locally there exists"—there might be a section on each open set that doesn't glue globally.

### Concrete Examples of Internal Reasoning

#### Example 1: Computing in Sheaves on $\mathbb{R}$

Working internally in $\text{Sh}(\mathbb{R})$:

```typescript
// External view: A sheaf of continuous functions
type ContFunc = Sheaf<(x: Real) => Real>

// Internal view: Just a function type!
type Func = Real → Real

// Internal theorem: All functions are continuous
theorem all_continuous: (f: Real → Real) → IsContinuous(f)
proof = -- Holds by the nature of the topos!

// But internally, we can't prove excluded middle:
// theorem fails: (P: Prop) → P ∨ ¬P
// because not every proposition corresponds to a clopen set
```

#### Example 2: Time-Dependent Truth in Presheaves

Consider $\mathbf{Set}^{\omega^{\text{op}}}$ where $\omega$ is the poset of natural numbers:

```typescript
// A type that "grows over time"
type Stream<A> = {
  at_time: (n: Nat) → List<A> // List of values known by time n
  monotone: (n ≤ m) → at_time(n) ⊆ at_time(m)
}

// Internal logic is temporal
theorem eventually_stable: 
  (s: Stream<Bool>) → ◇□(stable(s))
  where stable(s) = ∀n. s.at_time(n) = s.at_time(n+1)
  
// This uses temporal modalities:
// ◇P = "eventually P"
// □P = "always P from now on"
```

#### Example 3: Computability in the Effective Topos

In the effective topos, internal logic tracks computability:

```typescript
// Every function is computable
type Nat→Nat = ComputableFunction<Nat, Nat>

// Internal proof of a theorem gives an algorithm
theorem internal_minimum: 
  (P: Nat → Bool) → (∃n. P(n)) → Σ(n: Nat). P(n) ∧ (∀m. P(m) → n ≤ m)
  
// The internal proof actually computes the minimum!
// But we can't prove LPO (Limited Principle of Omniscience):
// ¬theorem: (f: Nat → Bool) → (∀n. f(n) = true) ∨ (∃n. f(n) = false)
```

### The Kripke-Joyal Semantics

The **Kripke-Joyal semantics** translates internal statements to external ones:

| Internal Statement      | External Meaning in $\text{Sh}(X)$                   |
| ----------------------- | ---------------------------------------------------- |
| $\phi \wedge \psi$      | $\phi$ and $\psi$ both hold                          |
| $\phi \vee \psi$        | Locally, either $\phi$ or $\psi$ holds               |
| $\phi \Rightarrow \psi$ | On any smaller open where $\phi$ holds, $\psi$ holds |
| $\forall x: A. \phi(x)$ | For all sections $x$ of $A$, $\phi(x)$ holds         |
| $\exists x: A. \phi(x)$ | Locally, there exists a section $x$ with $\phi(x)$   |

> [!note]
> **Forcing Relation**: For a sheaf topos $\text{Sh}(X)$, an open set $U$ forces a formula $\phi$ (written $U \Vdash \phi$) when $\phi$ holds on $U$ in the internal logic.

### Internal Categories and Higher Structures

Topoi can contain internal categories, leading to higher categorical structures:

```typescript
// Internal category in a topos E
type InternalCategory = {
  Objects: Type  // Object of objects
  Morphisms: Type  // Object of morphisms
  source, target: Morphisms → Objects
  identity: Objects → Morphisms
  compose: Pullback(source, target) → Morphisms
  // ... with appropriate axioms
}

// Example: Internal groupoid of paths in Sh(X)
type PathGroupoid = {
  Objects = Points  // Sheaf of points
  Morphisms = Paths  // Sheaf of paths
  // Internally, every morphism is invertible
  inverse: Morphisms → Morphisms
}
```

### Synthetic Mathematics

Working internally enables **synthetic** approaches where objects have inherent properties:

#### Synthetic Differential Geometry (SDG)
```typescript
// In the topos of smooth spaces
type D = {ε: Real | ε² = 0}  // Infinitesimals exist!

// Every function is infinitely differentiable
derivative<A,B>(f: A → B): A × D → B
derivative(f)(a, ε) = f(a + ε)  // Linear in ε by Kock-Lawvere

// We can define tangent bundles internally
type Tangent<M> = M × D
```

#### Synthetic Domain Theory
```typescript
// In a topos of domains
type Stream<A> = Nat → A

// All functions are continuous (preserve directed suprema)
theorem stream_continuity:
  (f: Stream<A> → B) → PreservesLimits(f)
  
// Fixed points exist for all endofunctions
fix: ((A → A) → A)
fix(f) = f(fix(f))  // Actually computable internally!
```

### Internal Modal Logic

Many topoi support internal modalities beyond classical logic:

```typescript
// In a cohesive topos
type Shape<A>     // Underlying shape/homotopy type
type Flat<A>      // Discrete type
type Sharp<A>     // Codiscrete type

// Adjoint modalities
flat_sharp_adjunction: Flat<A> → B ≃ A → Sharp<B>

// In presheaves over a group G
type Invariant<A> = {x: A | ∀g: G. g·x = x}
type Coinvariant<A> = A / ~  // where x ~ g·x
```

### Translation Between External and Internal

The relationship between external and internal viewpoints is given by:

1. **Externalization**: Internal statement $\phi$ ↦ External property "$1 \Vdash \phi$"
2. **Internalization**: External property of $A$ ↦ Internal statement about elements of $A$

> [!warning]
> **Not Everything Internalizes**: Some external properties (like "has a global section") may not have internal equivalents. The internal language captures only **geometric** properties.

### Practical Benefits

Working internally provides:
1. **Automatic continuity/computability** of all constructions
2. **Constructive proofs** that compute
3. **Modular reasoning** that respects the topos structure
4. **Synthetic proofs** that avoid technical details

## Applications to Type Theory

Topoi provide rich semantics for type theories, revealing deep connections between logic, computation, and geometry.

### Categorical Semantics of Dependent Types

Every topos $\mathcal{E}$ provides a model of dependent type theory through its **locally cartesian closed** structure.

#### Context Extension and Dependent Types

Contexts are interpreted as objects, and context extension as projection:

```
Γ, x: A ⊢     corresponds to     Γ.A → Γ
```

where $\Gamma.A$ is the object of pairs $(γ, a)$ with $γ: \Gamma$ and $a: A[γ]$.

#### Dependent Type Formers

> [!note]
> **Categorical Interpretation**:
> - **$\Pi$-types**: Right adjoint to weakening
>   $$\frac{\Gamma, x: A \vdash B(x) \text{ type}}{\Gamma \vdash \Pi(x: A). B(x) \text{ type}}$$
>   Interpreted as: $\Pi_f: \mathcal{E}/\Gamma.A \to \mathcal{E}/\Gamma$ where $f: \Gamma.A \to \Gamma$
>
> - **$\Sigma$-types**: Left adjoint to weakening  
>   $$\frac{\Gamma, x: A \vdash B(x) \text{ type}}{\Gamma \vdash \Sigma(x: A). B(x) \text{ type}}$$
>   Interpreted as: $\Sigma_f: \mathcal{E}/\Gamma.A \to \mathcal{E}/\Gamma$
>
> - **Identity types**: Diagonal functor
>   $$\frac{\Gamma \vdash a, b: A}{\Gamma \vdash \text{Id}_A(a, b) \text{ type}}$$
>   Interpreted as: Equalizer of $a, b: \Gamma \to A$

#### Example: Computing $\Pi$-types in Presheaves

In $\mathbf{Set}^{\mathcal{C}^{\text{op}}}$:

```typescript
// Given A: Γ → Type and B: Γ.A → Type
// The Pi-type is computed stage-wise:

(Π(x: A). B(x))(c) = ∏_{a ∈ A(c)} B(c, a)

// With restriction maps:
// For f: d → c, the restriction takes
// s ∈ (Π(x: A). B(x))(c) to
// λa. B(f)(s(A(f)(a)))
```

### Topos Models of Specific Type Theories

#### 1. Martin-Löf Type Theory (MLTT)

Requirements: Locally cartesian closed + additional structure

```typescript
// Natural numbers object (NNO)
type Nat = Zero | Succ(Nat)

// W-types (well-founded trees) require:
// - Polynomial functors preserve pullbacks
// - Initial algebras exist

// Universe hierarchies need:
// - Object classifier for small objects
// - Closure under type formers
```

> [!example]
> **Realizability Model**: The effective topos $\mathcal{E}\text{ff}$ models MLTT where:
> - Every function $\mathbb{N} \to \mathbb{N}$ is recursive
> - Proofs carry computational content
> - Axiom of Choice holds (constructively!)

#### 2. Homotopy Type Theory (HoTT)

The **simplicial set model** $\mathbf{sSet} = \mathbf{Set}^{\Delta^{\text{op}}}$:

```typescript
// Types are simplicial sets (∞-groupoids)
type Type = SimplicalSet

// Paths between points
Path: (A: Type) → (x y: A) → Type
Path(A)(x, y) = Hom_A(Δ¹, -)  // 1-simplices from x to y

// Higher paths
Path²: (A: Type) → (p q: Path(A)(x, y)) → Type
Path²(A)(p, q) = Hom_A(Δ², -)  // 2-simplices with boundary p, q

// Univalence axiom holds!
univalence: (A B: Type) → IsEquiv(idtoequiv : (A = B) → (A ≃ B))
```

Key features:
- Function extensionality holds
- Univalence interprets "equality of types" as equivalence
- Higher inductive types via left Kan extensions

#### 3. Guarded Recursive Type Theory

In the topos of **trees** $\mathbf{Set}^{\omega^{\text{op}}}$:

```typescript
// The later modality ▷
type Later<A> = {
  now: Empty  // No value available now
  step: A     // Value available one step later
}

// Guarded recursion
fix: <A>(f: Later<A> → A) → A
fix(f) = f(step(fix(f)))

// Productive corecursion
Stream<A> = A × Later<Stream<A>>
```

### Computational Effects via Topos Theory

Different topoi model different notions of computation:

#### 1. State and References

The **Schanuel topos** (presheaves on finite sets and injections):

```typescript
// Names/locations that can be allocated
type Ref<A> = Name

// State monad arises naturally
State<S, A> = S → (A × S)

// Fresh name generation
fresh: State<NameSupply, Ref<A>>
```

#### 2. Non-Determinism and Probability

The topos of **sheaves on measurable spaces**:

```typescript
// Probability distributions as subobjects
type Prob<A> = Subobject(A × [0,1])

// Probabilistic choice
choose: <A>(p: Real) → A → A → Prob<A>

// Conditional probability via restriction
condition: <A>(Prob<A>) → (A → Bool) → Prob<A>
```

#### 3. Continuity and Computability

The **effective topos** $\mathcal{E}\text{ff}$:

```typescript
// All functions are computable
computable: <A, B>(f: A → B) → Σ(e: Nat). IsIndex(e, f)

// Continuity at the type level
continuous: (f: Stream<Bool> → Bool) → 
  ∃n. ∀s,t: Stream<Bool>. (∀i < n. s[i] = t[i]) → f(s) = f(t)
```

### Internal Type Theory

Every topos has an internal type theory that can be extracted:

> [!note]
> **Mitchell-Bénabou Language**: The internal logic of a topos $\mathcal{E}$ is a dependent type theory with:
> - Types = Objects of $\mathcal{E}$
> - Terms = Generalized elements (morphisms from context)
> - Propositions = Subobjects
> - Proofs = Sections of subobjects

#### Extracting the Internal Language

Given a topos $\mathcal{E}$, we can define:

```
Types:      A type    ⟺   A ∈ Ob(E)
Terms:      Γ ⊢ t: A  ⟺   t: Γ → A in E
Props:      Γ ⊢ φ prop ⟺   φ ↪ Γ (subobject)
Proofs:     Γ ⊢ p: φ  ⟺   Γ → φ factors through φ ↪ Γ
```

#### Soundness and Completeness

> [!tip]
> **Key Results**:
> 1. **Soundness**: Every theorem in the internal logic is true in the topos
> 2. **Completeness** (for geometric theories): Every geometric sequent true in all topoi is derivable
> 3. **Incompleteness** (for general logic): Not all true statements are internally provable

### Parametricity and Relational Models

Presheaf topoi model parametric polymorphism:

#### The Parametricity Topos

For reflexive graphs $\mathcal{G} = \{• ⇉ •\}$, the topos $\mathbf{Set}^{\mathcal{G}^{\text{op}}}$:

```typescript
// Types with relations
type Relational<A> = {
  carrier: Type
  relation: carrier × carrier → Prop
  reflexive: ∀x. relation(x, x)
}

// Parametric functions preserve relations
parametric: <A, B>(f: A → B) → 
  ∀(R: Rel(A)). ∀(x, y: A). R(x, y) → f(x) ~B~ f(y)

// Free theorems from types!
theorem map_fusion:
  ∀(f: A → B)(g: B → C).
    map(g ∘ f) = map(g) ∘ map(f)
```

### Modal Type Theory in Topoi

Topoi with extra structure model modal type theories:

#### Cohesive Type Theory

In a cohesive topos with modalities $\flat \dashv \sharp$:

```typescript
// Discrete types (sets)
discrete: Type → Type = Flat

// Codiscrete types (spaces)  
codiscrete: Type → Type = Sharp

// Paths in discrete types are discrete
theorem discrete_paths:
  (A: Discrete(Type)) → Discrete(Path(A))

// Function types preserve discreteness
theorem discrete_exponential:
  Discrete(A) → Discrete(B) → Discrete(A → B)
```

### Bridge to Implementation

Topos models guide implementation of proof assistants:

1. **Normalization**: Use the topos model to prove normalization
2. **Decidability**: Check which type-checking problems are decidable
3. **Consistency**: Verify no inconsistencies in the type theory
4. **Computation**: Extract computational content from proofs

> [!example]
> **Cubical Type Theory**: Inspired by the cubical sets model
> - Implements univalence computationally
> - Path types compute via cubical structure
> - Validated against presheaf topos semantics

## Applications to Mathematics

### Synthetic Differential Geometry

In the topos of smooth spaces:
- Every function $\mathbb{R} \to \mathbb{R}$ is smooth
- Infinitesimals exist: $D = \{x \in \mathbb{R} : x^2 = 0\} \neq \{0\}$
- We can do calculus without limits!

> [!note]
> **Axiom**: In SDG topoi, we have the **Kock-Lawvere axiom**: Every function $f: D \to \mathbb{R}$ is linear, i.e., $f(d) = f(0) + d \cdot a$ for unique $a$.

### Forcing and Independence

Cohen's forcing translates to sheaf topoi:
- Start with a model of set theory (topos)
- Build a sheaf topos that "adds generic objects"
- Prove independence results by changing truth values

### Constructive Mathematics

Working internally in an arbitrary topos forces constructive reasoning:
- No excluded middle
- No axiom of choice (without additional structure)
- Proofs provide explicit constructions

## Advanced Topics: Going Deeper

### Classifying Topoi: The Universal Models

Classifying topoi provide a profound connection between logical theories and categorical structures. Every geometric theory has a classifying topos that serves as its "universal model."

#### What is a Geometric Theory?

A **geometric theory** $\mathbb{T}$ consists of:
- Sorts (basic types): $S_1, S_2, \ldots$
- Function symbols: $f: S_1 \times \cdots \times S_n \to S$
- Relation symbols: $R \subseteq S_1 \times \cdots \times S_n$
- Axioms using only: $\top, \wedge, \exists, =$ (no negation or universal quantification!)

> [!note]
> **Geometric Logic**: The fragment of first-order logic preserved by geometric morphisms:
> - Finite conjunctions: $\phi \wedge \psi$
> - Arbitrary disjunctions: $\bigvee_{i \in I} \phi_i$
> - Existential quantification: $\exists x. \phi(x)$
> - Equations: $t = s$
>
> Crucially, geometric logic is **preserved by inverse image functors** of geometric morphisms!

#### The Classifying Topos Construction

For a geometric theory $\mathbb{T}$, its classifying topos $\mathbf{Set}[\mathbb{T}]$ is constructed as:

```
𝐒𝐞𝐭[𝕋] = (Syntactic Category of 𝕋)^op
```

The objects are "definable sets" - formulas-in-context:
- $\{x: S | \phi(x)\}$ where $\phi$ is geometric
- Morphisms are provable functional relations

> [!example]
> **Example: The Theory of Groups**
> 
> Theory $\mathbb{G}$ has:
> - One sort: $G$
> - Operations: $e: 1 \to G$, $m: G \times G \to G$, $i: G \to G$
> - Axioms: associativity, identity, inverse (all geometric!)
>
> The classifying topos $\mathbf{Set}[\mathbb{G}]$ has:
> - Objects: Definable subsets of $G^n$ like $\{(x,y) | xy = e\}$
> - The generic group: The identity functor $G: \mathbf{Set}[\mathbb{G}] \to \mathbf{Set}$

#### Universal Property

The classifying topos satisfies a remarkable universal property:

> [!tip]
> **Classification Theorem**: For any topos $\mathcal{E}$, there is an equivalence:
> $$\text{GeomMor}(\mathcal{E}, \mathbf{Set}[\mathbb{T}]) \simeq \text{Models}_{\mathbb{T}}(\mathcal{E})$$
>
> Geometric morphisms into the classifying topos correspond precisely to models of the theory!

This means:
- $f: \mathcal{E} \to \mathbf{Set}[\mathbb{T}]$ gives a model $f^*(U_{\mathbb{T}})$ in $\mathcal{E}$
- Every model $M$ in $\mathcal{E}$ induces a unique (up to isomorphism) geometric morphism

#### Computing with Classifying Topoi

##### Example 1: Linear Orders

The theory $\mathbb{L}$ of linear orders:
```
Sorts: L
Relations: ≤ ⊆ L × L
Axioms: 
  - Reflexive: ∀x. x ≤ x
  - Transitive: ∀x,y,z. (x ≤ y ∧ y ≤ z) → x ≤ z  
  - Antisymmetric: ∀x,y. (x ≤ y ∧ y ≤ x) → x = y
  - Total: ∀x,y. x ≤ y ∨ y ≤ x
```

The classifying topos $\mathbf{Set}[\mathbb{L}]$ contains:
- The "generic linear order" with undecidable comparisons
- Definable subsets like intervals $[a,b] = \{x | a ≤ x ≤ b\}$
- The Dedekind real numbers arise as certain "cuts"

##### Example 2: Fields

For the theory of fields $\mathbb{F}$:
- The classifying topos contains the "generic field"
- Geometric morphisms $\mathbf{Set} \to \mathbf{Set}[\mathbb{F}]$ = field homomorphisms
- The generic field has "independent transcendentals"

#### Geometric Theories as Presentations

Every topos can be presented by a geometric theory:

> [!note]
> **Representation Theorem**: For any topos $\mathcal{E}$, there exists a geometric theory $\mathbb{T}_{\mathcal{E}}$ such that:
> $$\mathcal{E} \simeq \mathbf{Set}[\mathbb{T}_{\mathcal{E}}]$$
>
> The theory $\mathbb{T}_{\mathcal{E}}$ can be taken as the theory of "canonical sites" of $\mathcal{E}$.

This gives us a dictionary:
| Topos Concept | Theory Concept      |
| ------------- | ------------------- |
| Object        | Sort/Type           |
| Morphism      | Functional relation |
| Subobject     | Predicate           |
| Epimorphism   | Surjective function |
| Finite limit  | Equations           |

### Higher Topoi: The $\infty$-Categorical Perspective

The theory of topoi extends naturally to higher categories, yielding $(\infty,1)$-topoi.

#### What is an $(\infty,1)$-Topos?

An **$(\infty,1)$-topos** is an $(\infty,1)$-category that:
1. Has all small colimits
2. Has universal colimits (preserved by pullback)
3. Every groupoid object is effective
4. Every $\infty$-connected morphism has the descent property

> [!tip]
> **Intuition**: Replace "sets" with "spaces" or "$\infty$-groupoids":
> - Objects have higher homotopy/paths
> - Morphisms form spaces, not just sets
> - Subobjects are now "homotopy monomorphisms"

#### Key Examples

##### 1. $\infty$-Groupoids
The $(\infty,1)$-topos of spaces/Kan complexes:
- Objects: Homotopy types
- Morphisms: Continuous maps up to homotopy
- Models homotopy type theory

##### 2. $\infty$-Sheaves
For a site $(\mathcal{C}, J)$, the $(\infty,1)$-topos $\text{Sh}_{(\infty,1)}(\mathcal{C}, J)$:
- Objects: Stacks (sheaves of spaces)
- Morphisms: Natural transformations
- Crucial for derived algebraic geometry

##### 3. Parametrized Spectra
The stable $(\infty,1)$-topos of parametrized spectra:
- Objects: Families of spectra
- Models stable homotopy theory
- Connections to topological quantum field theory

#### Higher Modalities

$(\infty,1)$-topoi support richer modal operators:

```typescript
// Truncation modalities
τ_n: Type → Type  // n-truncation (kill homotopy above level n)

// Localization modalities
L_f: Type → Type  // f-localization (make f an equivalence)

// Cohesive modalities in cohesive ∞-topoi
ʃ: Type → Type   // Shape (fundamental ∞-groupoid)
♭: Type → Type   // Flat (discrete ∞-groupoid)
♯: Type → Type   // Sharp (codiscrete ∞-groupoid)
```

### Logical Functors and Morphisms

Beyond geometric morphisms, we have finer classifications:

#### Logical Functors

A functor $F: \mathcal{E} \to \mathcal{F}$ is **logical** if it preserves:
1. Finite limits (including terminal object)
2. Exponentials (power objects)
3. Subobject classifier
4. **And their Beck-Chevalley conditions**

> [!warning]
> **Rarity**: Logical functors are extremely rare! They require:
> - $F(\Omega_{\mathcal{E}}) \cong \Omega_{\mathcal{F}}$
> - Preservation of internal logic structure
> - Often only exist between Boolean topoi

#### Hyperconnected Morphisms

A geometric morphism $f: \mathcal{F} \to \mathcal{E}$ is **hyperconnected** if:
- $f^*$ is full and faithful
- $f^*$ reflects isomorphisms

These correspond to:
- Subtopoi with same objects but fewer morphisms
- Imposing additional "rigidity" constraints

#### Essential Subtopoi

An **essential subtopos** arises from a Lawvere-Tierney topology $j$:
- Objects: $j$-sheaves in original topos
- Inclusion has both left and right adjoints
- Examples: double-negation subtopos, closed/open subtopoi

### Modal Topoi and Axiomatic Cohesion

Some topoi come with additional modal structure:

#### Cohesive Topoi

A topos $\mathcal{E}$ is **cohesive** over $\mathbf{Set}$ if we have:

```
𝓔 ⟵⟶ Set
```

with quadruple adjunction: $\Pi \dashv \Delta \dashv \Gamma \dashv \nabla$

This models spaces with both discrete and continuous aspects:
- $\Pi$: Connected components
- $\Delta$: Discrete space
- $\Gamma$: Underlying set of points
- $\nabla$: Codiscrete space

#### Axiomatic Homotopy Theory

In an $(\infty,1)$-topos with suitable modalities, we can develop:
- Synthetic homotopy groups
- Synthetic homology/cohomology
- Synthetic stable homotopy theory

All without explicit constructions—the structure emerges from the axioms!

## Practical Consequences

Understanding topoi impacts how we:

1. **Design type systems**: Topoi guide which features combine well
2. **Prove independence**: Use different topoi as models
3. **Work constructively**: The internal language enforces constructivity
4. **Model computation**: Different topoi capture different effects

> [!tip]
> **For Type Theorists**: When designing a new type theory, ask "What topos models this?" The answer reveals semantic constraints and opportunities.

## Conclusion

Topos theory provides a flexible foundation where:
- Logic can be non-classical
- Computation and continuity intertwine  
- Abstract concepts have concrete models
- Type theory and category theory unite

Whether you're interested in the foundations of mathematics, the semantics of programming languages, or the nature of mathematical truth, topos theory offers profound insights and powerful tools.

The journey from elementary topoi to their applications spans decades of mathematical development, yet the core ideas remain elegantly simple: categories that behave like universes of sets, but with their own internal logic and structure.

## Further Reading

- **Gentle Introduction**: "Sheaves in Geometry and Logic" by Mac Lane & Moerdijk
- **Type Theory Focus**: "Categorical Logic and Type Theory" by Jacobs
- **Advanced**: "Sketches of an Elephant" by Johnstone (comprehensive reference)
- **Applications**: "Synthetic Differential Geometry" by Kock

## Exercises for the Curious

1. Show that in any topos, the subobject classifier $\Omega$ is injective
2. Prove that logical functors preserve the interpretation of intuitionistic logic
3. Find a topos where $\neg\neg P \to P$ fails for some proposition $P$
4. Construct a non-trivial geometric morphism between presheaf topoi