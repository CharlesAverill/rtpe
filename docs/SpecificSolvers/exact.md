---
title: "exact - RTPE"
---

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
