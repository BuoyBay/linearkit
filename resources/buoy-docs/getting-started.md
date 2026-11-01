---
title: "LinearKit first use"
summary: "Solve a pivoting system using the standalone console example."
category: "Guides"
order: 10
related: ["index.md", "api.md"]
---

# First use

Place `linearkit-0.1.0.buipkg` in your consumer's `packages/` directory, then compile
`examples/linearkit/main.bui` with `buoy main.bui -o app` and run `./app`.
The complete example solves the row-exchange system [[0,1],[1,0]] with b=[2,3],
then fits an intercept and slope to three observations with Householder QR.
The first solution is [3,2]; the fit is [7/6,1/2].

Always inspect the returned `Status` before reading `Solution`: failed solves have
Nil solutions. A small backward residual does not establish small forward error
for an ill-conditioned matrix. See [contracts](api.md) for tolerance and scaling.


Save the following as `main.bui` in your consumer project. Package archives and any dependencies must be installed as described above.

```buoy
Import linearkit
Sub Main()
    Dim a As New DenseMatrix(2, 2, [0.0, 1.0, 1.0, 0.0])
    Dim b As New Vector([2.0, 3.0])
    Dim solved As LinearSolveResult = Solve(a, b)
    Print solved.Status
    Print solved.Solution.At(0)
    Print solved.Solution.At(1)
    Print solved.ScaledResidual
    Dim design As New DenseMatrix(3, 2, [1.0, 0.0, 1.0, 1.0, 1.0, 2.0])
    Dim observations As New Vector([1.0, 2.0, 2.0])
    Dim fit As LinearSolveResult = LeastSquares(design, observations)
    Print fit.Status
    Print fit.Solution.At(0)
    Print fit.Solution.At(1)
End Sub
```
