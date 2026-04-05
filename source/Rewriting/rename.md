---
title: "rename - RTPE"
---

## rename

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
