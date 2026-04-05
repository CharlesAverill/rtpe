---
title: "Generalization - RTPE"
---

# [Generalization](/Generalization/index.html)

This group of tactics is often found at the beginnings of proofs. 
Generalization and its counterpart Specialization (both are included here) are concepts used to fine-tune how strong of a theorem is needed to continue.
Theorems that are too strong (specific) aren't useful for many different kinds of goals.
Theorems that are too weak (general) are frequently unprovable (even if their specified counterparts are!) and those that are provable are frequently harder to prove!


## [intros](/Generalization/intros.html)

Typically the first tactics a Rocq user ever utilizes.
`intros` finds assumptions builtin to your goal (usually in the form of a `forall` quantifier) and moves them to the goal's context (a.k.a. hypothesis space, assumption space).
This is similar to the first step of many informal, paper proofs, when the prover states "let there be some number n, ..."

More specifically, `intros` [specializes](/glossary.html#specialize) a goal by looking for [type inhabitation](/glossary.html#type_inhabitation) and proposition assumptions and moving them into the assumption space.
For example, if you write `forall (n : nat), n + 0 = n`, the `forall` is acting as an assumption that there is a value of type `nat` that we can call `n`.
Calling `intros` here will provide you an assumption `n` that there is a value of type `nat`.

`intros` will not introduce variables that are contained in opaque/wrapped definitions - <b>unless</b> an explicit name is provided for them.

A simpler tactic, `intro`, acts similarly but can only introduce one assumption, and will introduce variables contained in opaque/wrapped definitions.

### Syntax

```rocq
(* Simple usage - introduces all named assumptions *)
intros.

(* Give specific names to assumptions as you introduce *)
intros n m x.

(* Split a conjunction or existential assumption upon introducing *)
intros [A B].
```

### Examples

Before
```rocq
=========================
forall (n : nat), n + 0 = n
```

```rocq
intros x.
```

After
```rocq
x: nat
=========================
1/1
x + 0 = x
```

Before
```rocq
=========================
forall (A B C : Prop), A /\ B -> C -> A /\ C
```

```rocq
intros A B C [ATrue BTrue].
```

After
```rocq
A, B, C: Prop
ATrue: A
BTrue: B
=========================
1/1
C -> A /\ C
```

Before (assume `P := forall (n : nat), n = n`)
```rocq
=========================
1/1
P
```

```rocq
intros.
```

After
```rocq
=========================
1/1
P
```

Alternatively,

```rocq
intro.
```

After
```rocq
n: nat
=========================
1/1
n = n
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/tactics.html#rocq:tacn.intros)

<hr>


## [clear](/Generalization/clear.html)

`clear` erases assumptions from the assumption space.
Multiple assumptions may be erased in one tactic via a space-separated list of assumptions.
`clear` will fail if an assumption passed into it contains as subterms other variables that still exist in the goal state.

`clear - ...` can also be used to erase all assumptions <b>not depended on</b> by a provided set of assumptions.

### Syntax

```rocq
(* Simple usage *)
clear H.

(* Clear multiple assumptions *)
clear H Heq X Y n.

(* Clear anything that x, z, or c do not depend on *)
clear - x z c.
```

### Examples

Before
```rocq
n: nat
H, Hr1, Hr2: n = 0
IHn: n = 1
=========================
1/1
True
```

```rocq
clear Hr1 Hr2.
```

After
```rocq
n: nat
H: n = 0
IHn: n = 1
=========================
1/1
True
```

Before
```rocq
a, b, c, x, y, z: nat
H: a = z
=========================
1/1
True
```

```rocq
clear - a x H.
```

After
```rocq
a, x, z: nat
H: a = z
=========================
1/1
True
```
### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/tactics.html#rocq:tacn.tactic)

<hr>

<hr>
