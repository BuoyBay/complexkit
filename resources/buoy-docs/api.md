---
title: "Complex arithmetic API"
summary: "Public complexkit symbols and numerical contracts."
category: "Reference"
order: 20
keywords: ["complexkit", "API", "reference"]
symbols: ["ComplexNumber", "ComplexNumber.Real", "ComplexNumber.Imaginary", "ComplexNumber.Add", "ComplexNumber.Subtract", "ComplexNumber.Multiply", "ComplexNumber.Divide", "ComplexNumber.Conjugate", "ComplexNumber.Magnitude", "ComplexNumber.Argument", "ComplexNumber.Sqrt", "ComplexNumber.Exp", "ComplexNumber.Log", "ComplexNumber.Sin", "ComplexNumber.Cos", "ComplexNumber.Tan", "ComplexNumber.Sinh", "ComplexNumber.Cosh", "ComplexNumber.Tanh", "ComplexNumber.Asin", "ComplexNumber.Acos", "ComplexNumber.Atan", "ComplexNumber.Asinh", "ComplexNumber.Acosh", "ComplexNumber.Atanh", "ComplexNumber.Power", "ComplexFromPolar"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

`Import complexkit` exposes these public types and operations.

| Symbol | Behavior |
| --- | --- |
| `ComplexNumber(realPart As Double = 0.0, imaginaryPart As Double = 0.0)` | Create a validated finite value. |
| `ComplexNumber.Real / Imaginary As Double` | Writable components; later operations validate their current values. |
| `ComplexNumber.Add(other) / Subtract(other)` | Return a new sum or difference for a non-Nil complex operand. |
| `ComplexNumber.Multiply(other) / Divide(other)` | Return a new product or quotient; division by zero rejects. |
| `ComplexNumber.Conjugate()` | Return a new value with opposite imaginary component. |
| `ComplexNumber.Magnitude() As Double` | Scaled absolute magnitude; an overflowing result rejects. |
| `ComplexNumber.Argument() As Double` | Principal argument in radians; zero maps to zero. |
| `ComplexNumber.Sqrt() / Exp() / Log()` | Principal square root, complex exponential, or principal natural logarithm. |
| `ComplexNumber.Sin() / Cos() / Tan()` | Complex trigonometric functions; Tan composes Sin and Divide by Cos. |
| `ComplexNumber.Sinh() / Cosh() / Tanh()` | Hyperbolic functions with scaled products and large-real tanh. |
| `ComplexNumber.Asin() / Acos() / Atan()` | Principal inverse trigonometric functions. Atan rejects ±i. |
| `ComplexNumber.Asinh() / Acosh() / Atanh()` | Principal inverse hyperbolic functions. Atanh rejects ±1. |
| `ComplexNumber.Power(exponent As ComplexNumber)` | Return Exp(exponent multiplied by Log(self)); zero base rejects. |
| `ComplexFromPolar(radius As Double, angle As Double) As ComplexNumber` | Create a value from a finite nonnegative radius and finite angle in radians. |

## Numerical behavior

`Log` uses the principal argument from Atan2. `Sqrt` uses the principal root with a nonnegative real component; negative real inputs on the branch cut choose a positive imaginary component. Signed-zero branch distinctions are not promised. Scaled magnitude, division, logarithm, and square-root formulas reduce avoidable overflow, but this remains finite Double arithmetic. Underflow can become zero; exponential and trigonometric intermediates can overflow. There are no operator overloads, text parsers, implicit scalar operations, or tolerance-based equality.

## Errors and ownership

Constructors and methods reject nonfinite components, Nil operands, and overflowing computed values with `InvalidArgumentException`. Validation occurs again when methods read mutable components. Division by zero and logarithm of zero reject. Argument of zero is defined as zero, and square root of zero is zero. Power uses the principal logarithm and therefore rejects every zero base, even with a zero exponent.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)

[Full typed API: properties, parameters, defaults, and returns](typed-api.md)

## Extended branch and numerical contracts

The inverse functions accept every finite complex input except `Atanh(±1)`
and `Atan(±i)`, which reject with `InvalidArgumentException`. `Tanh` rejects
`±i*Math.Pi/2` and any input whose computed denominator is zero. Other odd
half-pi poles cannot in general be represented exactly in Double; argument
reduction and representational error can produce a large finite value near a
pole. No epsilon-based pole classification is used.

Exact cuts use deterministic conventions with zero treated as nonnegative:
`Asin` chooses nonnegative imaginary part, `Acos` nonpositive imaginary part,
`Asinh` nonnegative real part, `Acosh` nonnegative imaginary part, `Atanh`
nonnegative imaginary part and `Atan` nonnegative real part on their respective
cuts. Away from the cuts these are the usual principal analytic branches.
Signed-zero branch distinctions, Annex G bitwise parity, and correct rounding
are not promised. Existing `Sqrt` and `Log` conventions are unchanged.

The new hyperbolic products combine logarithmic scaling with trig factors when
needed; for example `Cosh(710)` remains finite although `Exp(710)` overflows.
`Tanh` uses a decaying exponential for large real parts. Inverses use scaled
elliptic coordinates, rationalized distance differences, small-argument log1p,
and logarithmic asymptotes to avoid overflow and cancellation. Subnormal results
can underflow or lose relative accuracy. Huge trigonometric arguments inherit
stdlib argument reduction accuracy. Existing `Sin`, `Cos`, `Tan`, arithmetic and
`Exp` retain their documented intermediate-overflow limits.
