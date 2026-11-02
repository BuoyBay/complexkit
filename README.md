# Complex numbers and principal elementary functions

Pure Buoy Double complex arithmetic inspired by [Roger Meier's Complex Utilities](https://opensource.the-meiers.org/).
`Import complexkit` exposes `ComplexNumber` and `ComplexFromPolar(radius, angle)`.
The package has no native dependencies. Methods return fresh objects and do not
modify their operands. The `Real` and `Imaginary` properties are writable.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add complexkit --git https://github.com/BuoyBay/complexkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

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

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer complexkit
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
