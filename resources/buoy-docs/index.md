---
title: "LinearKit dense linear algebra"
summary: "Finite vectors and row-major matrices, pivoted LU and Householder QR."
category: "Overview"
order: 0
keywords: ["linearkit", "vector", "matrix", "solve", "least squares"]
related: ["api.md", "getting-started.md"]
---

# LinearKit

Import `linearkit` from the sealed `linearkit-0.1.0.buipkg` in your project's
`packages/` directory. No native library dependency. The package provides finite
Double vectors and immutable row-major dense matrices with copied input/output.

Use `Solve` for square systems and `LeastSquares` for full-column-rank systems
with at least as many rows as columns. Singular and near-singular systems return
an explicit failure status. Invalid inputs and nonfinite arithmetic throw.
See [API and numerical contracts](api.md) and [first use](getting-started.md).
Only Linux x86-64 native execution has been tested; six desktop targets receive
semantic checks. No inverse, sparse, SVD, eigen or condition-number estimator.
