---
title: "repeat - RTPE"
---

## repeat

The `repeat` tactical repeatedly executes a tactic until it either fails or causes no change in the goal.
If the tactic provided succeeds, it will be recursively applied to each generated subgoal.

Be careful: if the input tactic never fails, `repeat` will cause an infinite loop!
For example, `repeat symmetry` or `repeat idtac` will always result in an infinite loop.

### Syntax

```rocq
(* Simple usage *)
repeat split.
```

### Examples

Before
```rocq
P, Q, R, S: Prop
=========================
1/1
P /\ Q /\ R /\ S
```

```rocq
repeat split.
```

After
```rocq
P, Q, R, S: Prop
=========================
1/4
P
=========================
2/4
Q
=========================
3/4
R
=========================
4/4
S
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/ltac.html#rocq:tacn.repeat)
