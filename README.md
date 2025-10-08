# UN Algebra: Uncertainty Between Actual, Tolerance, and Measurement

## Overview

**UN Algebra** (Uncertainty-Nominal Algebra) extends N/U Algebra to capture the uncertainty inherent in the relationship between three reference frames:

- **0ₐ**: Actual value (ground truth, often unknown)
- **0ₜ**: Tolerance specification (engineering/design bounds)
- **0ₘ**: Platform measurement (observed value from sensors)

## Core Concept

The fundamental insight: **The value lies between 0ₐ and 0ₘ, with uncertainty governed by tolerances (0ₜ) and measurement platform capabilities (Pₘ)**.

### Mathematical Framework (Tentative)

**Representation**: UN value as ordered triple or tensor

```
UN = (0ₐ, 0ₜ, 0ₘ, Pₘ)
```

Where:
- `0ₐ`: Actual/true value (may be unknown)
- `0ₜ`: Engineering tolerance (e.g., ±0.01mm)
- `0ₘ`: Measured value from platform
- `Pₘ`: Platform measurement uncertainty

### Fundamental Inequality

```
|0ₘ - 0ₐ| ≥ 0
```

**Interpretation**: The measurement uncertainty is itself uncertain when we lack either:
- The actual reference (0ₐ), OR
- The tolerance reference (0ₜ)

This creates a **second-order uncertainty** - we're uncertain about the uncertainty.

### Tentative Algebraic Structure

**Possibility 1: Quadratic form**
```
UN(x) = α·0ₐ² + β·0ₜ² + γ·0ₘ² + δ·Pₘ²
```

**Possibility 2: Tensor form**
```
UN = [ 0ₐ   0ₜ  ]
     [ 0ₘ   Pₘ  ]
```

**Possibility 3: Nested N/U pairs**
```
UN = ((0ₐ, 0ₜ), (0ₘ, Pₘ))
  where inner pairs are N/U values
```

## Motivation

### Engineering Reality

In manufacturing/robotics:
1. **Design specifies**: Bolt diameter = 10mm ± 0.05mm (0ₐ ≈ 10mm, 0ₜ = 0.05mm)
2. **Caliper measures**: 10.03mm ± 0.01mm (0ₘ = 10.03mm, Pₘ = 0.01mm)
3. **Question**: Is the bolt within tolerance?

**Classical approach**: Compare |0ₘ - 0ₐ| ≤ 0ₜ

**Problem**: We don't know 0ₐ (only 0ₘ), and Pₘ may be comparable to 0ₜ!

**UN Algebra approach**: Propagate uncertainty through all three reference frames.

### AI/ML Context

When training data has:
- **Ground truth labels** (0ₐ) - may be noisy or biased
- **Annotation guidelines** (0ₜ) - tolerance for inter-rater agreement
- **Model predictions** (0ₘ) - measured output
- **Test set uncertainty** (Pₘ) - finite sample effects

UN Algebra would quantify: "How confident are we that the model satisfies the annotation standard?"

## Open Questions

1. **Algebraic operations**: How do UN values compose?
   - Addition: UN₁ ⊕ UN₂ = ?
   - Multiplication: UN₁ ⊗ UN₂ = ?

2. **Reduction to N/U**: When can we collapse UN → (n, u)?
   - If 0ₐ is known: (0ₐ, √(0ₜ² + Pₘ²))
   - If 0ₐ unknown: (0ₘ, 0ₜ + Pₘ) (conservative)

3. **Measurement**: What is the "nominal" of a UN value?
   - Best estimate: 0ₘ (what we measured)
   - Or weighted: w₁·0ₐ + w₂·0ₘ (if 0ₐ known)

4. **Invariants**: What properties should hold?
   - |0ₘ - 0ₐ| ≤ 0ₜ + Pₘ (triangle inequality)
   - If Pₘ → 0, UN reduces to (0ₐ, 0ₜ)
   - If 0ₜ → 0, UN reduces to (0ₐ, Pₘ)

## Connection to N/U Algebra

**N/U Algebra** (Martin, 2025) represents values as:
```
(n, u) where n = nominal, u = uncertainty
```

**UN Algebra** extends this to handle:
- **Unknown nominals** (0ₐ may not be accessible)
- **Dual uncertainty sources** (tolerance vs. measurement)
- **Reference frame ambiguity** (which is "nominal"?)

### Reduction Formula (Proposed)

```
UN → N/U projection:
(n, u) = (0ₘ, |0ₘ - 0ₐ| + Pₘ)  if 0ₐ known
(n, u) = (0ₘ, 0ₜ + Pₘ)          if 0ₐ unknown (conservative)
```

## Status

🚧 **Pre-alpha conceptual framework**

- Mathematical formalism: TBD
- Implementation: Not started
- Validation: Not started

## References

- **N/U Algebra**: Martin, E. et al. (2025). DOI: [10.5281/zenodo.17222201](https://doi.org/10.5281/zenodo.17222201)
- **Discussion**: [UN Algebra Extension Thread](https://github.com/abba-01/nualgebra_anthropology/discussions/3) on nualgebra_anthropology

## Contributing

This is an exploratory concept. Contributions welcome via:
1. Mathematical formalization proposals
2. Use case examples (engineering, AI, metrology)
3. Connections to existing frameworks (interval arithmetic, affine arithmetic, Dempster-Shafer)

## License

TBD
