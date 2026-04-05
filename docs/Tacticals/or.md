---
title: "|| - RTPE"
---

## [||](/Tacticals/or.html)

The infix `||` tactical tries the first tactic and only tries the second if the first failed.
In other words, `||` executes the first tactic that makes progress on the goal.

### Syntax

```rocq
(* Simple usage *)
reflexivity || assumption.
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
reflexivity || assumption.
```

After
```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/ltac.html#first-tactic-to-make-progress)

<hr>
