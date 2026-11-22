# Lean verification for Cycle 6

## What this checks

`Cycle6.lean` formalizes the core real-variable optimization argument:

- the reduction from the four cross-sum constraints to `u + v >= d/3`;
- the four-case lower bound `max(L1, L2) >= 23*d/75`;
- the resulting algebraic exponent conversion to `52*d/75`;
- equality on the proposed tight dimension ray;
- the elementary exponent identity from rectangular blocking.

The file contains no axioms and no `sorry` placeholders.

## What it does not check

It does not formalize or verify:

- the external rectangular matrix-multiplication exponent theorem `omega(1,2,1) <= 25/8`;
- the existence and rational coefficient-height bounds of a finite recursive bilinear scheme;
- bit-complexity of the full rational implementation;
- the set-multilinear heavy-gate decomposition or the PIT algorithm;
- any statement about `P` versus `NP`.

These are separate obligations. A successful Lean build validates the optimization proof only, not the whole research note.

## Requirements and test command

Use Lean 4 with Mathlib available in the project. From the project directory, run:

```bash
lake env lean Cycle6.lean
```

The current execution environment used to prepare these files did not contain a Lean executable, so this file has **not been compiled here**. It is provided as a checkable Lean/Mathlib proof script, not as a claim that a Lean build has already succeeded.
