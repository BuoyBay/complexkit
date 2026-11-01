# ComplexKit 0.1.0

Pure Buoy Double complex arithmetic inspired by [Roger Meier's Complex Utilities](https://opensource.the-meiers.org/).
`Import complexkit` exposes `ComplexNumber` and `ComplexFromPolar(radius, angle)`.
The package has no native dependencies. Methods return fresh objects and do not
modify their operands. The `Real` and `Imaginary` properties are writable.

## API

`New ComplexNumber(realPart = 0.0, imaginaryPart = 0.0)` creates a value.
`Add`, `Subtract`, `Multiply`, `Divide` accept another `ComplexNumber`.
`Conjugate`, `Sqrt`, `Exp`, `Log`, `Sin`, `Cos`, `Tan`, `Sinh`, `Cosh`,
`Tanh`, `Asin`, `Acos`, `Atan`, `Asinh`, `Acosh`, `Atanh` return a complex value.
`Power(exponent)` uses `Exp(exponent * Log(self))`. `Magnitude` returns a Double;
`Argument` returns radians. `ComplexFromPolar` requires a nonnegative radius.

Components must be finite. Constructors and methods reject NaN, infinities,
Nil operands and overflowing computed values with `InvalidArgumentException`.
Because properties are mutable, validation also occurs when methods read them.
Division by zero and logarithm of zero reject. `Argument(0)` is defined as zero;
`Sqrt(0)` is zero. `Power` rejects a zero base, including exponent zero.
`Log` uses the principal argument from `Atan2`; `Sqrt` uses the principal root
with nonnegative real part, choosing positive imaginary part for negative real
inputs on the branch cut. Signed-zero branch distinctions are not promised.

Magnitude, division, logarithm and square root use scaled formulas to avoid
squaring large components directly. This is finite Double arithmetic, not
arbitrary precision or a correctly rounded complex library. Underflow can become
zero; trigonometric and exponential intermediates may overflow even when a
rearranged formula could produce a finite result. There are no tolerance-based
equality, text parsing, implicit scalar arithmetic or operator overloads.

## Build and verify

Maintainers run the private validation suite before release. See the repository README for public build instructions.

The sealed local artifact is `packages/complexkit-0.1.0.buipkg`. It has not been
published to a registry. See [provenance and original parity](../PROVENANCE.md).

## Extended principal functions

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

Maintainers run the private validation suite before release. See the repository README for public build instructions.
