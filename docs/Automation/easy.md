---
title: easy - RTPE
---

## [easy](/Automation/easy.html)

`easy` throws many common "closing tactics" at a goal to solve a large category of simple problems.
`easy` will attempt to use:

- [`trivial`](/RTPE/Automation/trivial.html)

- [`reflexivity`](/RTPE/SpecificSolvers/reflexivity.html)

- [`symmetry`](/RTPE/Rewriting/symmetry.html)

- [`contradiction`](/RTPE/SpecificSolvers/contradiction.html)

- [`inversion`](/RTPE/CaseAnalysis/inversion.html)

- [`intros`](/RTPE/Generalization/intros.html)

- [`split`](/RTPE/Simplification/split.html) (this begins a recursive call of `easy`)

- [`destruct`](/RTPE/CaseAnalysis/destruct.html) (on hypotheses with conjunctions)

`easy` is the base form of the [`now`](/RTPE/Tacticals/now.html) tactical.

### Syntax

```rocq
easy.
```

### Examples

Before
```rocq
P: Prop
H: P
=========================
1/1
True /\ 42 = 14 * 3 /\ P
```

```rocq
easy.
```

After
```rocq
No more goals.
```

### Resources

[Reference Documentation](https://rocq-prover.org/doc/master/refman/proofs/automatic-tactics/auto.html#rocq:tacn.easy)

<hr>
