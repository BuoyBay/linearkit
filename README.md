# Vectors, matrices, solvers

Source-only finite Double vectors, dense matrices, and linear solves. Copy the sealed
`packages/linearkit-0.1.0.buipkg` into a consumer's `packages/`, then `Import linearkit`.
No native dependencies. All numeric inputs and computed public outputs must be finite.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add linearkit --git https://github.com/BuoyBay/linearkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
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

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer linearkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```


## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
