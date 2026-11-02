---
title: "Complex arithmetic getting started"
summary: "Use complexkit with a complete example and explicit numerical conventions."
category: "Guides"
order: 10
keywords: ["complexkit", "example", "import"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

## Prepare the package

Place the sealed `complexkit-0.1.0.buipkg` archive in your project's `packages/` directory. The example imports the package by its manifest name and uses explicit methods.

## First use

Construct complex operands or call `ComplexFromPolar`, then retain the fresh results from arithmetic methods. Angles are radians. Read `Magnitude()` and `Argument()` for polar reporting.

```basic
Import complexkit

Sub Main()
    Dim impedance As New ComplexNumber(3.0, 4.0)
    Dim voltage As New ComplexNumber(12.0, 0.0)
    Dim current As ComplexNumber = voltage.Divide(impedance)
    Print current.Real
    Print current.Imaginary
    Print current.Magnitude()
    Dim negative As New ComplexNumber(-9.0, 0.0)
    Dim root As ComplexNumber = negative.Sqrt()
    Print root.Imaginary
End Sub
```

The package also provides `Sinh`, `Cosh`, `Tanh`, `Asin`, `Acos`, `Atan`,
`Asinh`, `Acosh` and `Atanh`. See the API reference for their exact-cut
conventions, poles and scaled numerical behavior.

## Conventions

`Log` uses the principal argument from Atan2. `Sqrt` uses the principal root with a nonnegative real component; negative real inputs on the branch cut choose a positive imaginary component. Signed-zero branch distinctions are not promised. Scaled magnitude, division, logarithm, and square-root formulas reduce avoidable overflow, but this remains finite Double arithmetic. Underflow can become zero; exponential and trigonometric intermediates can overflow. There are no operator overloads, text parsers, implicit scalar operations, or tolerance-based equality.

## Handle invalid inputs

Constructors and methods reject nonfinite components, Nil operands, and overflowing computed values with `InvalidArgumentException`. Validation occurs again when methods read mutable components. Division by zero and logarithm of zero reject. Argument of zero is defined as zero, and square root of zero is zero. Power uses the principal logarithm and therefore rejects every zero base, even with a zero exponent.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
