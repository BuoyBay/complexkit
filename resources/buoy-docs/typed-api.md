---
title: "complexkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["ComplexNumber"]
dependencies: []
symbols: ["ComplexNumber"]
related: ["api.md", "getting-started.md", "index.md"]
---

# complexkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## ComplexNumber

`Public Class ComplexNumber`

Double precision complex arithmetic; methods return fresh values.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Real` | `Double` | No | No | `0.0` | — |
| `Imaginary` | `Double` | No | No | `0.0` | — |

### Constructor

`Public Sub Constructor(realPart As Double = 0.0, imaginaryPart As Double = 0.0)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `realPart` | `Double` | `ByVal` | `0.0` |
| `imaginaryPart` | `Double` | `ByVal` | `0.0` |

Returns: no value.

### Add

`Public Function Add(other As ComplexNumber) As ComplexNumber`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `ComplexNumber` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Subtract

`Public Function Subtract(other As ComplexNumber) As ComplexNumber`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `ComplexNumber` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Multiply

`Public Function Multiply(other As ComplexNumber) As ComplexNumber`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `ComplexNumber` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Divide

`Public Function Divide(other As ComplexNumber) As ComplexNumber`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `other` | `ComplexNumber` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Conjugate

`Public Function Conjugate() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Magnitude

`Public Function Magnitude() As Double`

No parameters.

#### Returns

| Type |
| --- |
| `Double` |

### Argument

`Public Function Argument() As Double`

Principal argument in radians; the convention for zero is zero.

No parameters.

#### Returns

| Type |
| --- |
| `Double` |

### Exp

`Public Function Exp() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Log

`Public Function Log() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Sqrt

`Public Function Sqrt() As ComplexNumber`

Principal square root; negative real inputs use the positive imaginary root.

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Sin

`Public Function Sin() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Cos

`Public Function Cos() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Tan

`Public Function Tan() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Sinh

`Public Function Sinh() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Cosh

`Public Function Cosh() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Tanh

`Public Function Tanh() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Asin

`Public Function Asin() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Acos

`Public Function Acos() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Asinh

`Public Function Asinh() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Acosh

`Public Function Acosh() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Atanh

`Public Function Atanh() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Atan

`Public Function Atan() As ComplexNumber`

No parameters.

#### Returns

| Type |
| --- |
| `ComplexNumber` |

### Power

`Public Function Power(exponent As ComplexNumber) As ComplexNumber`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `exponent` | `ComplexNumber` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `ComplexNumber` |

## ComplexKit functions

### ComplexFromPolar

`Public Function ComplexFromPolar(radius As Double, angle As Double) As ComplexNumber`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `radius` | `Double` | `ByVal` | Required |
| `angle` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `ComplexNumber` |
