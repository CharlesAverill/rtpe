---
title: symmetry - RTPE
---

## [symmetry](/rtpe/Rewriting/symmetry.html)

`symmetry` is used to swap the left and right sides of an equality.

`symmetry` can be used on either the goal or a list of hypotheses.

### Syntax

```rocq
(* Usage on goal *)
symmetry.

(* Usage on hypotheses *)
symmetry in H.
symmetry in H1, H2.
```

### Examples

Before
```rocq
=========================
1/1
5 = 2 + 3
```

```rocq
symmetry.
```

After
```rocq
=========================
1/1
2 + 3 = 5
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/equality.html#rocq:tacn.symmetry)

<hr>
