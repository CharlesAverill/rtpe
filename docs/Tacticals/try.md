---
title: "try - RTPE"
---

## [try](/ctpe/Tacticals/try.html)

The `try` tactical executes a provided tactic, catching any errors and always succeeding.

### Syntax

```rocq
(* Simple usage *)
try reflexivity.
```

### Examples

Before
```rocq
n: nat
=========================
1/1
n + 0 = n
```

```rocq
try reflexivity.
```

After
```rocq
n: nat
=========================
1/1
n + 0 = n
```

Alternatively,

```rocq
try apply add_0_r.
```

```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/ltac.html#rocq:tacn.try)

<hr>
