---
title: "reflexivity - RTPE"
---

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
