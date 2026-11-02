---
title: "LinearKit API and numerical contracts"
summary: "Exact ownership, dimensions, tolerance and residual policies."
category: "Reference"
order: 20
symbols: ["Vector", "DenseMatrix", "LinearSolveResult", "Solve", "LeastSquares"]
related: ["index.md", "getting-started.md"]
---

## API and ownership

- `New Vector(values As Array Of Double)` copies 1..4096 components. Read-only
  `Count`, checked `At(index)`, copied `ToArray()`. `Add`, `Subtract`, `Scale`,
  `Dot`, `Norm`, `Normalize`, and three-component `Cross`. Zero normalization rejects.
- `New DenseMatrix(rows, columns, values)` copies row-major data. Dimensions are
  1..4096, with at most 65536 elements. The product is checked before multiplying.
  Read-only `Rows`, `Columns`, checked `At(row,column)`, copied `ToArray()`.
  `Add`, `Subtract`, `Scale`, `Transpose`, `Multiply`, `MultiplyVector` return fresh values.
- `Solve(a As DenseMatrix, b As Vector, tolerance As Double = 1e-12)` uses LU
  elimination with partial row pivoting, for square matrices.
- `LeastSquares(a, b, tolerance = 1e-12)` uses unpivoted Householder QR for m >= n;
  it never forms normal equations. Both solvers allow at most 256 unknowns.
- `LinearSolveResult.Status` is `Success`, `Singular` (LU), or `RankDeficient` (QR).
  On success, `Solution` is an immutable Vector. On failure it is Nil and
  `ScaledResidual` is -1. The result properties are read-only. Its public constructor
  is a data carrier; only results returned by the solvers carry solver guarantees.

Dimension mismatches, invalid indices, Nil operands, nonfinite values, arithmetic
overflow and invalid tolerances throw `InvalidArgumentException`. A tolerance must
be finite and strictly between 0 and 1. LU rejects any pivot <= tolerance times
max(abs(A)); QR rejects any R diagonal on that same scale. Both A and b are first
scaled together by max(max(abs(A)), max(abs(b))). Extremely disparate scales may
underflow during scaling and cause conservative failure. These tests are explicit
numerical rank policies, not estimates of a condition number. A success does not
promise accurate forward error for an ill-conditioned system. Raising tolerance
rejects more systems; lowering it can accept unreliable ones. QR is not rank
revealing and has no column pivoting, SVD, minimum-norm or underdetermined solve.

`ScaledResidual` is the infinity-norm backward residual
`||Ax-b||inf / (||A||inf * ||x||inf + ||b||inf)` (zero if denominator is zero),
computed with common scaling to limit overflow. For least squares it measures the
remaining fit residual, so it need not be tiny. It is not a rank/condition test or
a forward-error bound. Summations and residuals have ordinary Double rounding.

Norm and normalization use scaling to avoid squaring large components; Normalize
can succeed even when the mathematical norm exceeds Double range. Dot uses
Neumaier compensated products/sums, falling back to scaled operands and binary
rescaling when products/sums overflow. Underflow, loss of tiny terms relative to
huge terms, and product rounding remain possible; this is not an exact dot product
or a correctly rounded numerical library. Cross uses the same compensated/scaled
two-term dot products, allowing cancellation of overflowing individual products.
Matrix products use the same dot policy. All operations leave operands unchanged.
