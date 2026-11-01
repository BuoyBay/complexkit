---
title: "Complex arithmetic"
summary: "Work with finite Double complex numbers and principal elementary functions."
category: "Overview"
order: 0
keywords: ["complexkit", "mathematics", "numerical"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# Complex arithmetic

`complexkit` supplies explicit complex arithmetic methods and elementary functions without a native dependency. Methods return fresh `ComplexNumber` objects and never mutate their operands; the component properties themselves are writable.

## Install

Copy `complexkit-0.1.0.buipkg` into the consuming application's `packages/` directory and use `Import complexkit`. The package is independently usable on macOS, Windows, and Linux. It requires no native bridge or drawing surface.

## Scope and provenance

This is an independent implementation inspired by Roger Meier's Complex Utilities, with explicit Buoy methods rather than drop-in operator or source API compatibility. Principal inverse trigonometric and hyperbolic functions are included. Formatting, scalar-wrapper, and other original APIs remain outside this package.

## Validation and limits

Constructors and methods reject nonfinite components, Nil operands, and overflowing computed values with `InvalidArgumentException`. Validation occurs again when methods read mutable components. Division by zero and logarithm of zero reject. Argument of zero is defined as zero, and square root of zero is zero. Power uses the principal logarithm and therefore rejects every zero base, even with a zero exponent.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
