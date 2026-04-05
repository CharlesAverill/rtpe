---
title: "Simplification - RTPE"
---

# [Simplification](/rtpe/Simplification/index.html)

This group of tactic aims to reduce the complexity of terms in a goal. 
They will not solve a goal, only convert it into what is a structurally smaller (although maybe not lexically smaller!) form of the original goal.


## [simpl](/rtpe/Simplification/simpl.html)

`simpl` evaluates terms that are constructed of constant values - not variables.
`simpl` can also partially evaluate partially-constant values.

### Syntax

```rocq
(* Simplify the goal as much as possible *)
simpl.

(* Simplify a hypothesis *)
simpl in H.

(* Simplify in the entire proof state *)
simpl in *.

(* Only simplify a specific term in a specific hypothesis *)
simpl (2 + 2) in H.
```

### Examples

Before
```rocq
=========================
1/1
2 + 2 = 1 + 3
```

```rocq
simpl (2 + 2).
```

After
```rocq
=========================
1/1
4 = 1 + 3
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/equality.html#rocq:tacn.simpl)

<hr>


## [unfold](/rtpe/Simplification/unfold.html)

`unfold` replaces definition identifiers with the definition's contents, simplifying along the way.

### Syntax

```rocq
(* Simple example *)
unfold plus.

(* Unfolding a definition in a hypothesis *)
unfold X in H.

(* Unfolding a definition in all hypotheses and the goal *)
unfold X in *.
```

### Examples

Given
```rocq
Fixpoint bitlist (n : nat) : list bool :=
    match n with
    | O =>    true  :: nil
    | S n' => false :: (bitlist n')
    end.
```

Before
```rocq
n: nat
l: list bool
H: bitlist (S (S n)) = false :: false :: l
=========================
1/1
bitlist (S n) = false :: l
```

```rocq
unfold bitlist in *.
```

After
```rocq
n: nat
l: list bool
H: false
     :: false
        :: (fix bitlist (n : nat) : list bool :=
              match n with
              | 0 => true :: nil
              | S n' => false :: bitlist n'
              end) n =
    false :: false :: l
=========================
1/1
false
 :: (fix bitlist (n0 : nat) : list bool :=
       match n0 with
       | 0 => true :: nil
       | S n' => false :: bitlist n'
       end) n = false :: l
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/equality.html#rocq:tacn.unfold)

<hr>


## [split](/rtpe/Simplification/split.html)

`split` is primarily used to break a single goal of the form `A /\ B` into two new goals `A` and `B`.

You will often notice that `split` seems to solve some of the subgoals that it generates.
This is because `split` is just shorthand for `constructor 1` (see the [`constructor` tactic](/RTPE/CaseAnalysis/constructor.html)).

Looking at the definition of `/\` (or `and`):
```rocq
Inductive and (A B : Prop) : Prop :=  conj : A -> B -> A /\ B.
```
we can see that `and` has a single constructor called `conj` - so `constructor 1` simply reduces to `apply conj`, which would give us goals `A` and `B` due to the impliciations that it carries.

### Syntax

```rocq
split.
```

### Examples

Before
```rocq
=========================
1/1
True /\ False
```

```rocq
split.
```

After
```rocq
=========================
1/2
True
=========================
2/2
False
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/reasoning-inductives.html#rocq:tacn.split)

<hr>

<hr>
