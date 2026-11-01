# Source and scope

Source: [Complex Utilities 1.0](https://opensource.the-meiers.org/ComplexUtils_v1.0.zip),
linked from [Roger Meier’s project page](https://opensource.the-meiers.org/).
The page states that its source code is public domain. Download inspected
2026-10-31; ZIP SHA-256 `800723d15a117ee4417595c185873af174dbbc5dcdf5f3e2fe829b0bb7c11862`.

Inspected archive contents: `Complex.rbo`, `ComplexWrappers.rbo`, the binary
`ComplexUtils Testbench.rbp`, and `ComplexUtils Documentation.txt`. The latter
was read in full to map the public API. The RBO files have the `RbBF` binary
container header; binary source implementation was not treated as plain text
or claimed to have been fully decoded. No upstream source files are vendored.
This is an independent implementation of the documented mathematical behavior.

| Original | Buoy implementation |
| --- | --- |
| Real/Imag properties, numeric constructors | Real/Imaginary, Double constructor |
| +, -, *, / operators and mixed real operands | Explicit Add/Subtract/Multiply/Divide methods, complex operands |
| Abs, Arg, Conj | Magnitude, Argument, Conjugate |
| Pol2Rect | ComplexFromPolar |
| Sqrt, Exp, Log, Sin, Cos, Tan | Principal elementary methods |
| Complex power | Power via principal logarithm |
| String constructor, Str/CStr/Format | Deferred |
| Inv, Norm and scalar wrappers | Compose Divide and component arithmetic; no named parity methods |
| Sinh/Cosh/Tanh, Asin/Acos/Atan, Asinh/Acosh/Atanh | Principal finite-component methods |
| Cot, Sec, Cosec | Deferred |
| Operator overloads and implicit conversion | Deferred |
| Original GUI testbench | Console example and automated mathematical tests |

A focused math package fills a reusable Double complex arithmetic gap without
requiring renderer or OS bridges. The original complete API remains a larger
compatibility project. Tests verify this package’s stated semantics, not binary
parity with the original testbench.

## Extended algorithms (independently written)

No external implementation source was copied or translated for these additions.
The formulas were derived from elementary complex identities. For `asin(x+iy)`,
let `r=hypot(|x|+1,|y|)`, `s=hypot(|x|-1,|y|)` and `alpha=(r+s)/2`.
The real angle is `atan2(x,sqrt(alpha-|x|)*sqrt(alpha+|x|))`; the imaginary
magnitude is `acosh(alpha)`. `acos` uses the complementary atan2 directly,
avoiding subtraction from pi/2 near an endpoint. Rationalize each distance
increment using `hypot(u,b)-u=b*(b/(hypot(u,b)+u))`. Retain `alpha-1`
and the square root of `alpha-|x|` independently so rounding alpha to one
does not erase small components. For tiny b below an interior real point,
the imaginary height is `b/sqrt((1-|x|)*(1+|x|))`; at the endpoints it is
`sqrt(b)`. For components over 1e150 the neglected inverse-square correction
is below Double precision: use the directional atan2 and `log(hypot)+log(2)`.

`asinh(z)=-i asin(i z)`, `acosh` rotates the principal acos result with the
side of the imaginary component, and `atan(z)=-i atanh(i z)`. The atanh real
part is `log1p(4*|x|/((1-|x|)^2+y^2))/4`, using log distance differences
near a pole and a reciprocal scaled asymptote for huge inputs. Its imaginary
part uses `atan2(2*|y|,1-x^2-y^2)/2`. The private positive log1p evaluates
`2*(t+t^3/3+...+t^13/13)`, `t=x/(2+x)`, below 0.01; the omitted term
is below rounding error there.

Sinh/cosh products use ordinary real hyperbolics below 20 and
`sign*exp(|x|-log(2)+log(|factor|))` above it (the omitted exponential
correction is below Double precision). Tanh uses a sum of squares for small
real parts and `exp(-2*|x|)` scaling for large ones. All public results pass
through the existing finite-component constructor. Python stdlib `cmath` is
an independent test oracle, not implementation source or a runtime dependency.

A second test oracle uses Python Decimal at 100 digits: real hyperbolics from
exp(±x), inverse hyperbolics from real log/sqrt identities, and inverse trig
from a real atan alternating series after half-angle reduction. Pi is evaluated
with Machin's identity `16*atan(1/5)-4*atan(1/239)`. This independently checks
axis values and rotations without calling cmath. Test tolerances allow Double
rounding and documented subnormal loss; they do not establish correct rounding.
