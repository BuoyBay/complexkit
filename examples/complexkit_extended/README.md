# ComplexKit inverse hyperbolic round trip

`main.bui` computes `Asinh()` for a complex value and applies `Sinh()` to recover
its real and imaginary components within a small floating-point tolerance.
It prints `ComplexKit inverse hyperbolic round trip passed` when the comparison
succeeds.

Install the package into a consumer project, copy this `main.bui` beside that
project's `packages/` directory, then compile and run it with Buoy. This console
example does not require a GUI or a native math library.
