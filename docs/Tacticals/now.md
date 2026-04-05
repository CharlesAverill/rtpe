---
title: now - RTPE
---

## [now](/Tacticals/now.html)

`now tactic` is simply notation for `tactic;` [`easy`](/RTPE/Automation/easy.html).

### Syntax

```rocq
now split.
```

### Examples

Before
```rocq
=========================
1/1
True /\ 42 = 14 * 3
```

```rocq
now split.
```

After
```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/automatic-tactics/auto.html#rocq:tacn.now)

<hr>
