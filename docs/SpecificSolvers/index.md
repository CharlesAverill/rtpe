---
title: "Specific Solvers - RTPE"
---

# [Specific Solvers](/rtpe/SpecificSolvers/index.html)

Each tactic in this group exists to solve a very specific kind of goal.
They're fairly simple to learn about and use, because their goal targets are such small groups that there are hardly any degrees of freedom for automation to be required.
Essentially all Rocq proofs include some of these (whether they're written by the programmer or called by more complex tactics).


## [reflexivity](/rtpe/SpecificSolvers/reflexivity.html)

`reflexivity` solves goals which state that a term is equal to itself.
`reflexivity` has some simplification power, but not as much as [`simpl`](/RTPE/Simplification/simpl.html).
This tactic will fail if it cannot solve the goal.

`reflexivity` makes an attempt to simplify the goal and then `apply eq_refl`, where `eq_refl` is the sole constructor of the `eq` Inductive Proposition, stating that `forall {A : Type} (a : A), eq a a`.

### Syntax

```rocq
(* Simple usage *)
reflexivity.
```

### Examples

Before
```rocq
n: nat
=========================
1/1
n = n
```

```rocq
reflexivity.
```

After
```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/equality.html#rocq:tacn.reflexivity)

<hr>


## [assumption](/rtpe/SpecificSolvers/assumption.html)

`assumption` solves goals in which there exists an assumption that directly proves the goal (no simplification).
This tactic will fail if there does not exist such an assumption.

### Syntax

```rocq
(* Simple usage *)
assumption.
```

### Examples

Before
```rocq
P: Prop
H: P
=========================
1/1
P
```

```rocq
assumption.
```

After
```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/tactics.html#rocq:tacn.assumption)

<hr>


## [discriminate](/rtpe/SpecificSolvers/discriminate.html)

`discriminate` solves goals that are trivial inequalities (something of the form `x <> y`)\*.
This tactic will fail if the goal is not an inequality or is non-trivial.

\* Keep in mind that `x <> y` is actually shorthand for `x = y -> False`! 
This means that `discriminate` actually searches for trivial inequalities in assumptions.

### Syntax

```rocq
(* Simple usage *)
discriminate.
```

### Examples

Before
```rocq
=========================
1/1
1 <> 2
```

```rocq
discriminate.
```

After
```rocq
No more goals.
```

Before
```rocq
=========================
1/1
"hello" <> "world"
```

```rocq
discriminate.
```

After
```rocq
No more goals.
```

Before
```rocq
H: S n = O
==========================
1/1
False
```

```rocq
discriminate.
```

After
```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/reasoning-inductives.html#rocq:tacn.discriminate)

<hr>


## [exact](/rtpe/SpecificSolvers/exact.html)

`exact` allows users to solve goals by providing a proof object directly.
This tactic will fail if the provided proof object does not prove the goal.

### Syntax

```rocq
(* Simple usage *)
exact I.
```

### Examples

Before
```rocq
=========================
1/1
True
```

```rocq
exact I.
```

After
```rocq
No more goals.
```

Before
```rocq
n: nat
=========================
1/1
n + 5 = n + 5
```

```rocq
exact (eq_refl (n + 5)).
```

After
```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/tactics.html#rocq:tacn.exact)

<hr>


## [contradiction](/rtpe/SpecificSolvers/contradiction.html)

`contradiction` solves goals in which there exist contradictory hypotheses.
These contradictions generally take the form of a `False` hypothesis or a pair of hypotheses that state `P` and `~ P` for some proposition.
This tactic will fail if no such contradictions exist.

### Syntax

```rocq
(* Simple usage *)
contradiction.
```

### Examples

Before
```rocq
H: False
=========================
1/1
False
```

```rocq
contradiction.
```

After
```rocq
No more goals.
```

Before
```rocq
x, y: nat
H: x = y
H0: x <> y
=========================
1/1
x = x + y
```

```rocq
contradiction.
```

After
```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/tactics.html#rocq:tacn.contradiction)

<hr>

<hr>
