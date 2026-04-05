---
title: idtac - RTPE
---

## [idtac](/rtpe/Automation/idtac.html)

`idtac` leaves a goal completely unchanged. This tactic will never fail.

A term can be provided as an argument to print a message to the console.
String and integers are printed literally rather than via their type's pretty-printer.

`idtac` is sometimes useful when you have many goals selected and only want to operate on some of them.

### Syntax

```rocq
(* Simple usage *)
idtac.

(* Print a message *)
idtac "Hello World!".
```

### Examples

Before
```rocq
=========================
1/1
True
```

```rocq
idtac.
```

After
```rocq
=========================
1/1
True
```

Before
```rocq
n: nat
=========================
1/1
n + 0 = n
```

```rocq
(* Only apply reflexivity to the n = 0 case. Leave the n = S n' case unaffected *)
induction n; [reflexivity | idtac].
```

After
```rocq
n : nat
IHn : n + 0 = n
=========================
1/1
S n + 0 = S n
```
### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/ltac.html#rocq:tacn.idtac)

<hr>
