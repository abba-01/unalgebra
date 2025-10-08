# UN Algebra: Uncertainty Between Actual, Tolerance, and Measurement

## Concept

Extending N/U Algebra to handle uncertainty when we lack reference frames:

**Three reference points**:
- **0ₐ**: Actual value (ground truth, often unknown)
- **0ₜ**: Tolerance specification (engineering/design bounds)
- **0ₘ**: Measured value (platform observation)
- **Pₘ**: Platform measurement uncertainty

## Fundamental Insight

```
|0ₘ - 0ₐ| ≥ 0
```

This inequality is **itself uncertain** when we don't have:
- The actual reference (0ₐ), OR
- The tolerance reference (0ₜ)

This creates **second-order uncertainty** - we're uncertain about the uncertainty.

## Proposed Algebraic Structures

### Option 1: Quadratic Form
```
UN(x) = α·0ₐ² + β·0ₜ² + γ·0ₘ² + δ·Pₘ²
```

### Option 2: Tensor Form
```
UN = [ 0ₐ   0ₜ  ]
     [ 0ₘ   Pₘ  ]
```

### Option 3: Nested N/U Pairs
```
UN = ((0ₐ, 0ₜ), (0ₘ, Pₘ))
```
where each inner pair is an N/U value.

## Example: Manufacturing

**Scenario**: Check if bolt meets specification

1. **Design**: Diameter = 10mm ± 0.05mm (0ₐ ≈ 10mm, 0ₜ = 0.05mm)
2. **Measurement**: Caliper reads 10.03mm ± 0.01mm (0ₘ = 10.03mm, Pₘ = 0.01mm)
3. **Question**: Is bolt within tolerance?

**Classical**: Compare |0ₘ - 0ₐ| ≤ 0ₜ
**Problem**: We don't know 0ₐ (only 0ₘ), and Pₘ ≈ 0ₜ!

**UN Algebra**: Propagate uncertainty through all three reference frames.

## Connection to N/U Algebra

**Reduction formula** (proposed):
```
UN → N/U projection:
(n, u) = (0ₘ, |0ₘ - 0ₐ| + Pₘ)  if 0ₐ known
(n, u) = (0ₘ, 0ₜ + Pₘ)          if 0ₐ unknown (conservative)
```

## Open Questions

1. What are the algebraic operations (⊕, ⊗)?
2. When can UN be reduced to (n,u)?
3. What invariants must hold?
4. How does this relate to affine arithmetic / zonotopes?

## Repository

https://github.com/abba-01/unalgebra

**Status**: Pre-alpha conceptual framework (mathematical formalism TBD)

Feedback and collaboration welcome!
