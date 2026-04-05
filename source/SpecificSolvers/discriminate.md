---
title: "discriminate - RTPE"
---

## discriminate

`discriminate` solves goals that are trivial inequalities (something of the form `x <> y`)\*.
This tactic will fail if the goal is not an inequality or is non-trivial.

\* Keep in mind that `x <> y` is actually shorthand for `x = y -> False`! 
This means that `discriminate` actually searches for trivial inequalities in assumptions.

### Syntax

```rocq
(* Simple usage *)
discriminate.
```

### Examples

Before
```rocq
=========================
1/1
1 <> 2
```

```rocq
discriminate.
```

After
```rocq
No more goals.
```

Before
```rocq
=========================
1/1
"hello" <> "world"
```

```rocq
discriminate.
```

After
```rocq
No more goals.
```

Before
```rocq
H: S n = O
==========================
1/1
False
```

```rocq
discriminate.
```

After
```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/reasoning-inductives.html#rocq:tacn.discriminate)
