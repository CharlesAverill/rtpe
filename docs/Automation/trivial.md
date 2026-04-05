---
title: "trivial - RTPE"
---

## [trivial](/Automation/trivial.html)

`trivial` is essentially a non-recursive [`auto`](/RTPE/Automation/auto.html).
`trivial` is best utilized when a lemma that exactly matches the goal already exists in the hint database.

### Syntax

```rocq
(* Simple usage *)
trivial.

(* Using a specific database *)
trivial with bool.
```

### Examples

Script
```rocq
Theorem trivial_example : forall {X : Type} (n : X), 
    n = n.
Proof.
    trivial.
Qed.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/automatic-tactics/auto.html#rocq:tacn.trivial)

<hr>
