---
title: "linearkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["DenseMatrix", "LinearSolveResult", "Vector"]
dependencies: []
symbols: ["DenseMatrix", "LinearSolveResult", "Vector"]
related: ["api.md", "getting-started.md", "index.md"]
---

# linearkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## Vector

`Public Class Vector`

Immutable finite vector of 1..4096 components; copies input and output arrays.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Count` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(values As Array Of Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `values` | `Array Of Double` | `ByVal` | Required |

Returns: no value.

### At

`Public Function At(index As Integer) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `index` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### ToArray

`Public Function ToArray() As Array Of Double`

No parameters.

#### Returns

| Type |
| --- |
| `Array Of Double` |

### Add

`Public Function Add(other As Vector) As Vector`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `Vector` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Vector` |

### Subtract

`Public Function Subtract(other As Vector) As Vector`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `Vector` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Vector` |

### Scale

`Public Function Scale(factor As Double) As Vector`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `factor` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Vector` |

### Dot

`Public Function Dot(other As Vector) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `Vector` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### Norm

`Public Function Norm() As Double`

No parameters.

#### Returns

| Type |
| --- |
| `Double` |

### Normalize

`Public Function Normalize() As Vector`

No parameters.

#### Returns

| Type |
| --- |
| `Vector` |

### Cross

`Public Function Cross(other As Vector) As Vector`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `Vector` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Vector` |

## DenseMatrix

`Public Class DenseMatrix`

Row-major immutable finite matrix. Dimensions 1..4096, at most 65536 elements.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Rows` | `Integer` | Yes | No | — | — |
| `Columns` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(rows As Integer, columns As Integer, values As Array Of Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `rows` | `Integer` | `ByVal` | Required |
| `columns` | `Integer` | `ByVal` | Required |
| `values` | `Array Of Double` | `ByVal` | Required |

Returns: no value.

### At

`Public Function At(row As Integer, column As Integer) As Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `row` | `Integer` | `ByVal` | Required |
| `column` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### ToArray

`Public Function ToArray() As Array Of Double`

No parameters.

#### Returns

| Type |
| --- |
| `Array Of Double` |

### Add

`Public Function Add(other As DenseMatrix) As DenseMatrix`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `DenseMatrix` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `DenseMatrix` |

### Subtract

`Public Function Subtract(other As DenseMatrix) As DenseMatrix`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `DenseMatrix` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `DenseMatrix` |

### Scale

`Public Function Scale(factor As Double) As DenseMatrix`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `factor` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `DenseMatrix` |

### Transpose

`Public Function Transpose() As DenseMatrix`

No parameters.

#### Returns

| Type |
| --- |
| `DenseMatrix` |

### Multiply

`Public Function Multiply(other As DenseMatrix) As DenseMatrix`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `DenseMatrix` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `DenseMatrix` |

### MultiplyVector

`Public Function MultiplyVector(other As Vector) As Vector`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `Vector` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Vector` |

## LinearSolveResult

`Public Class LinearSolveResult`

Status is Success, Singular or RankDeficient. Failure has Nil Solution and residual -1.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Status` | `String` | Yes | No | — | — |
| `Solution` | `Vector` | Yes | No | — | — |
| `ScaledResidual` | `Double` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(status As String, solution As Vector, scaledResidual As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `status` | `String` | `ByVal` | Required |
| `solution` | `Vector` | `ByVal` | Required |
| `scaledResidual` | `Double` | `ByVal` | Required |

Returns: no value.

### Solve

`Public Function Solve(a As DenseMatrix, b As Vector, tolerance As Double = 0.000000000001) As LinearSolveResult`

LU elimination with partial row pivoting; rejects pivots <= tolerance * max(abs(A)).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `a` | `DenseMatrix` | `ByVal` | Required |
| `b` | `Vector` | `ByVal` | Required |
| `tolerance` | `Double` | `ByVal` | `0.000000000001` |

#### Returns

| Type |
| --- |
| `LinearSolveResult` |

### LeastSquares

`Public Function LeastSquares(a As DenseMatrix, b As Vector, tolerance As Double = 0.000000000001) As LinearSolveResult`

Unpivoted Householder QR; m >= n. Rejects R diagonals relative to max(abs(A)).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `a` | `DenseMatrix` | `ByVal` | Required |
| `b` | `Vector` | `ByVal` | Required |
| `tolerance` | `Double` | `ByVal` | `0.000000000001` |

#### Returns

| Type |
| --- |
| `LinearSolveResult` |
