---
title: fail - RTPE
---

## [fail](/ctpe/Automation/fail.html)

`fail` always fails.

This is sometimes useful if you're building a complex tactic with try-catch behavior.

### Syntax

```rocq
(* Simple usage *)
fail.
```

### Examples

Before
```rocq
=========================
1/1
True
```

```rocq
fail.
```

After
```rocq
Error: Tactic failure.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proof-engine/ltac.html#rocq:tacn.fail)

<hr>
