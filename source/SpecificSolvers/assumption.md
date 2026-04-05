---
title: "assumption - RTPE"
---

## assumption

`assumption` solves goals in which there exists an assumption that directly proves the goal (no simplification).
This tactic will fail if there does not exist such an assumption.

### Syntax

```rocq
(* Simple usage *)
assumption.
```

### Examples

Before
```rocq
P: Prop
H: P
=========================
1/1
P
```

```rocq
assumption.
```

After
```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/tactics.html#rocq:tacn.assumption)
