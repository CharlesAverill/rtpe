---
title: "remember - RTPE"
---

## [remember](/Rewriting/remember.html)

`remember` gives a name to complex terms.
Specifically, `remember t` (where `t` has type `T`) introduces an assumption that there exists a member of type `T`, gives it a name such as `t0`, and provides another assumption that `t = t0`.

### Syntax

```rocq
(* Simple usage *)
remember (5 + x).

(* Provide a name for the remembered term *)
remember ("hello world") as s.
```

### Examples

Before
```rocq
x, y: nat
H: x + y = x
=========================
1/1
y = 0
```

```rocq
remember (x + y) as sum.
```

After
```rocq
x, y, sum: nat
Heqsum: sum = x + y
H: sum = x
=========================
1/1
y = 0
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/tactics.html#rocq:tacn.remember)

<hr>
