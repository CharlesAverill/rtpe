---
title: tactic - CTPE
---

## tactic

A short summary of what the tactic does, starting the most generally and ending the most specifically.

### Syntax

```rocq
(* Example 1 *)
tactic argument in H with x.

(* Example 2 *)
tactic -> t.
```

### Examples

Before
```rocq
n: nat
=========================
1/2
False
=========================
2/2
True
```

```rocq
tactic n.
```

After
```rocq
n: nat
=========================
1/2
True
=========================
2/2
True
```

Script
```rocq
Theorem test : 
    forall (n : nat), False /\ True.
Proof.
    tactic n. all: auto.
Qed.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/tactics.html#rocq:tacn.tactic)
