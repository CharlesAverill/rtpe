---
title: "destruct - RTPE"
---

## [destruct](/ctpe/CaseAnalysis/destruct.html)

`destruct` allows for case analysis on inductive terms or assumptions.
It can be used to split assumptions with conjunctions and disjunctions, as well as existential assumptions.
The arguments of `destruct` are [patterns](/ctpe/glossary.html#pattern).

### Syntax

```rocq
(* Simple usage *)
destruct H.

(* Destruct a term and introduce a hypothesis E showing its equivalence to the form it took *)
destruct n eqn:E.

(* Providing names for newly-introduced terms *)
destruct H as [H0 [H1 H2]].

(* Providing only some names for newly-introduced terms *)
destruct H as [H0 [? H1]].

(* Destructing multiple terms/hypotheses *)
destruct x as [| x0 x1], H as [[H1 H0] H2].

(* Providing names for newly-introduced terms in different generated subgoals *)
destruct H as [H1 | H2].
```

### Examples

Before
```rocq
n: nat
=========================
n = 0 \/ 1 <= n
```

```rocq
destruct n as [| n'] eqn:E.
```

After (first goal generated)
```rocq
n: nat
E: n = 0
=========================
1/2
0 = 0 \/ 1 <= 0
```

After (second goal generated)
```rocq
n, n': nat
E: n = S n'
=========================
2/2
S n' = 0 \/ 1 <= S n'
```

Script
```rocq
Theorem destruct_example1 : forall n : nat,
    n = 0 \/ 1 <= n.
Proof.
    intros. destruct n as [| n'] eqn:E.
    - left. reflexivity.
    - right. apply le_n_S, le_0_n.
Qed.
```

Script
```rocq
Theorem destruct_example2 : forall (P Q R : Prop),
    ((P /\ Q) /\ R) -> P /\ (Q /\ R).
Proof.
    intros P Q R H.
    destruct H as [[PTrue QTrue] RTrue]. split.
    - apply PTrue.
    - split. 
        -- apply QTrue.
        -- apply RTrue.
Qed.
```

Script
```rocq
Theorem destruct_example3 : 
    forall (P Q R : Prop),
    (P \/ Q) -> P \/ Q \/ R.
Proof.
    intros. destruct H as [PTrue | QTrue].
    - left. assumption.
    - right. left. assumption.
Qed. 
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/reasoning-inductives.html#rocq:tacn.destruct)

<hr>
