---
title: "constructor - RTPE"
---

## [constructor](/ctpe/CaseAnalysis/constructor.html)

When faced with a goal consisting of an inductive proposition with multiple constructors (such as [`le`](https://rocq-prover.org/doc/master/corelib/Corelib.Init.Peano.html#le) or [`NoDup`](https://rocq-prover.org/doc/master/stdlib/Stdlib.Lists.List.html#NoDup)), the `constructor` tactic iteratively attempts to apply each inductive constructor until one makes progress.

This tactic can succeed in multiple ways. Consider the following scenario:

```rocq
Inductive example : nat -> Prop :=
| EOdd (n : nat) :
    even n = false ->
    example n
| EEven (n : nat) :
    even n = true ->
    example n.

Goal forall n, even n = true -> example n.
Proof.
    intros.
    constructor;
    (* This will print out:
        even n = false
        even n = true
       as `constructor` first tries to prove
       the goal via EOdd, `assumption` fails,
       and then we backtrack and try EEven *)
    match goal with 
    | [|- ?G] => idtac G; assumption
    end.
```

Binding values to specific names is supported, as with `apply`.

### Syntax

```rocq
(* Simple usage *)
constructor.

(* Bind to variables in the applied constructor *)
constructor with (n := S x) (m := 5).
```

### Examples

Before
```rocq
n: nat
=========================
n = 0 \/ 1 <= n
```

```rocq
constructor.
```

After (`or_introl` applied)
```rocq
n: nat
=========================
n = 0
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/reasoning-inductives.html#rocq:tacn.constructor)

<hr>
