---
title: "contradiction - RTPE"
---

## [contradiction](/ctpe/SpecificSolvers/contradiction.html)

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
