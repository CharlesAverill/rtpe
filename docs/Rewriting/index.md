---
title: "Rewriting - RTPE"
---

# [Rewriting](/Rewriting/index.html)

This group of tactics is very frequently used in the middles of proofs.
Rewriting in all of its forms is an efficient way to bring together previously-independent parts of a goal.


## [rewrite](/Rewriting/rewrite.html)

`rewrite` takes an equivalence proof as input, like `t1 = t2`, and replaces all occurances of `t1` with `t2`.
Replacement of `t2` with `t1` can be achieved with the variant `rewrite <-` (rewrite backwards).
Multiple rewrites can be chained with one tactic via a list of comma-separated equivalence proofs.
Each of the equivalence proofs in the chain may be rewritten backwards.
`rewrite` will fail if there are no `t1`'s (in this example) to replace.

### Syntax

```rocq
(* Replace t1 with t2 in the goal *)
rewrite t1_eq_t2.

(* Rewrite in an assumption *)
rewrite Eq in H.

(* Rewrite in the goal and all assumptions *)
rewrite HEq in *.

(* Rewrite multiple values *)
rewrite t1_eq_t2, <- x_eq_y, ht_eq_ht.
```

### Examples

Before
```rocq
x, y: nat
H: x = y
=========================
x + y = y + y
```

```rocq
rewrite H.
```

After
```rocq
x, y: nat
H: x = y
=========================
y + y = y + y
```

Alternatively,
```rocq
rewrite <- H.
```


```rocq
x, y: nat
H: x = y
=========================
x + x = x + x
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/writing-proofs/equality.html#rocq:tacn.rewrite)

<hr>


## [rename](/Rewriting/rename.html)

`rename` changes the name of an introduced variable or assumption.

### Syntax

```rocq
(* Simple example *)
rename x into y.
```

### Examples

Before
```rocq
n: nat
=========================
1/1
n = n
```

```rocq
rename n into x.
```

After
```rocq
x: nat
=========================
1/1
x = x
```
### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/tactics.html#rocq:tacn.rename)

<hr>


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


## [symmetry](/Rewriting/symmetry.html)

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

<hr>
