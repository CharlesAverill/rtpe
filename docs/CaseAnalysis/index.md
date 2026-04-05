---
title: "Case Analysis - RTPE"
---

# [Case Analysis](/ctpe/CaseAnalysis/index.html)

Case analysis is a core aspect of constructivist logic.
Although for many kinds of problems it is a low-level tool, it is ubiquitous among the foundations of all problems formalized in the Rocq system.
The core idea is: "if I want to prove a property P holds for a term t, I can do so by writing multiple sub-proofs stating that for each form that t can have, P holds."


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


## [inversion](/ctpe/CaseAnalysis/inversion.html)

`inversion` looks at a given piece of structural evidence and draws conclusions from it.
If there are multiple sets of conclusions, `inversion` will generate a new proof obligation for each one.
Informally, `inversion` is doing a more specific form of the case analysis provided by [`destruct`](destruct.html) - where `destruct` essentially says "I don't know what this term is, so I'll prove a property for all of the possible forms of it," `inversion` says "I know exactly what terms could construct this hypothesis because of its definition, so I'll only prove a property for those terms."

This tactic often generates many trivial equality assumptions that may clutter the assumption space. 
I recommend almost always following `inversion` with [`subst`](/) to immediately substitute away these equalities.

### Syntax

```rocq
(* Standard usage *)
inversion H.
```

### Examples

Before
```rocq
n: nat
H: n <= 1
=========================
1/1
n = 0 \/ n = 1
```

```rocq
inversion H.
```

After (first goal generated):

Note: this is the case of `n <= 1` where `n = 1`, hence `H0`.
```rocq
n: nat
H: n <= 1
H0: n = 1
=========================
1/2
1 = 0 \/ 1 = 1
```

After (second goal generated):

Note: this is the case of `n <= 1` where `n < 1`, equivalent to `n <= 0`, hence `H1`.
```rocq
n: nat
H: n <= 1
m: nat
H1: n <= 0
H0: m = 0
=========================
1/1
n = 0 \/ n = 1
```

Script
```rocq
Theorem inversion_example1 : 
    forall n, n <= 1 -> n = 0 \/ n = 1.
Proof.
    intros. inversion H. 
    - right. reflexivity.
    - inversion H1. left. reflexivity.
Qed.
```

Script
```rocq
Inductive color : Type :=
| Red | Blue | Green | Cyan | Magenta | Yellow.

Inductive makes_white : color -> color -> color -> Prop :=
| RBG : makes_white Red Blue Green
| CMY : makes_white Cyan Magenta Yellow.

Theorem inversion_example2 : 
    forall (c1 c2 c3 : color),
    makes_white c1 c2 c3 ->
    (c1 = Red /\ c2 = Blue /\ c3 = Green) \/
    (c1 = Cyan /\ c2 = Magenta /\ c3 = Yellow).
Proof.
    intros c1 c2 c3 Hmw. inversion Hmw. 
    - left. repeat split.
    - right. repeat split.
Qed.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/reasoning-inductives.html#rocq:tacn.inversion)

<hr>


## [induction](/ctpe/CaseAnalysis/induction.html)

`induction` is an extension of `destruct` that allows for case analysis on inductive terms, gaining an inductive hypothesis for each recursive subterm generated by the term destruction.
The arguments of `induction` are [patterns](/RTPE/glossary.html#pattern).

If the goal still contains named impliciations, `induction` can be used before introducing them with [intros](/RTPE/Generalization/intros.html).
In this case, if the argument to `induction` is not the first impliciation in the chain, all implications before it will be introduced to the goal's assumption space.

`induction` can act similarly to `inversion` under specific circumstances.
If you induct over an object that already contains subterms, you can [remember](/RTPE/Rewriting/remember.html) the subterm(s) and induct on the root object. Then, by an easy `inversion` on the hypothesis generated by `remember`, all cases that don't match the required form generated by the case analysis will be automatically solved by the [principle of explosion](/RTPE/glossary.html#explosion).

Sometimes, the automatically-generated induction principles for a type are not sufficient to prove some properties about terms with that type. 
In this case, it is possible to write a [custom induction principle](https://softwarefoundations.cis.upenn.edu/lf-current/IndPrinciples.html) for a type and then use it with the `induction` tactic.

### Syntax

```rocq
(* Simple usage *)
induction n.

(* Induct over a term and introduce a hypothesis E showing its equivalence to the form it took *)
induction n eqn:E.

(* Providing names for newly-introduced terms *)
induction n as [| n' IHn' ].

(* Using a custom induction principle *)
induction z using peano_ind.
```

### Examples

Before
```rocq
n: nat
=========================
n + 0 = n
```

```rocq
induction n as [| n' IHn' ].
```

After (first goal generated)
```rocq
=========================
1/2
0 + 0 = 0
```

After (second goal generated)
```rocq
n': nat
IHn' : n' + 0 = n'
=========================
1/1
S n' + 0 = S n'
```

Script
```rocq
Theorem induction_example1 : forall (n : nat),
    n + 0 = n.
Proof.
    induction n.
    - reflexivity.
    - simpl. rewrite IHn. reflexivity.
Qed.
```

Script
```rocq
Require Import ZArith.
Open Scope Z.
Theorem induction_example2 : forall (x y : Z),
    x + y = y + x.
Proof.
    induction x using Z.peano_ind.
    - intros. simpl. rewrite Z.add_0_r. reflexivity.
    - intros. rewrite Z.add_succ_l. rewrite IHx.
      rewrite Z.add_comm. rewrite <- Z.add_succ_l.
      rewrite Z.add_comm. reflexivity.
    - intros. rewrite Z.add_pred_l. rewrite IHx.
      rewrite Z.add_comm. rewrite <- Z.add_pred_l.
      rewrite Z.add_comm. reflexivity.
Qed. 
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/reasoning-inductives.html#rocq:tacn.induction)

["Induction Principles" - Logical Foundations](https://softwarefoundations.cis.upenn.edu/lf-current/IndPrinciples.html)

<hr>


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

Furthermore, a specific constructor's index can be supplied to specifically apply that one.

### Syntax

```rocq
(* Simple usage *)
constructor.

(* Bind to variables in the applied constructor *)
constructor with (n := S x) (m := 5).

(* Apply the 5th constructor in the type's constructor list *)
constructor 5.
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

<hr>
