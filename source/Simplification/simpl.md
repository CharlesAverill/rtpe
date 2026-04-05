---
title: "simpl - RTPE"
---

## simpl

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
