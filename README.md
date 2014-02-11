SplineLibrary
=============
A C++ library to collect many useful spline functions into one place.

A spline is a formula for smoothly transitioning from one data point to the next in a data set. For example, you could create a spline containing ten colors (each stored as R, G, and B values) to create a color gradient that smoothly transitions from one color to the next.

Features
-------------
* Interpolation of standard catmull-rom splines
    * Include `spline_library/cubic_hermite/cr_spline.h`, create a `CRSpline` object, and call its `getPosition` method.
    * Several more spline types. See [Spline Types](docs/SplineTypes.md) for the full list
* Looping Splines
    * To make a looping catmull-rom spline, include `spline_library/cubic_hermite/looping_cr_spline.h` and create a `LoopingCRSpline` object instead.
    * Every spline type has both looping and non-looping variants
* Compute the inverse of a spline
    * Given a data point (not necessarily on the spline, or even close to it), what T value brings the spline closest to that data point?
    * Create a SplineInverter object and call either its findClosestFast or findClosestPrecise method
* Interpolation of the first, second, and third derivatives of the spline
    * The first derivative is called the "tangent" - this is how quickly and in what direction the interpolated position is changing, per T
    * The second derivative is called the "curvature" - this is how quickly and in what direction the interpolated tangent is changing, per T
    * The third derivative is called the "wiggle" - this is how quickly and in what direction the interpolated curvature is changing, per T
    

Documentation
-------------
[Glossary](docs/Glossary.md) - Glossary of important terms for understanding splines.

[Spline class API](docs/SplineAPI.md) - API documentation of the `Spline` base class.

[Spline Types](docs/SplineTypes.md) - Complete list of all supported spline formulas

[Spline Utilities](docs/SplineUtilities.md) - Documentation of some utility classes for splines, including `SplineInverter` and `SplineLengthCalculator`.

Project Layout
-------------
The root of the repository is a Qt Creator project that demonstrates some uses of the library. The source for the spline code itself is in the "spline_library" directory, and the code to set up the demo is in the "demo" directory.

The demo project requires Qt 5. To build it, either run qmake with the .pro file to generate a makefile, or open the .pro file in qt Creator.

The spline_library code has no third-party dependencies, so it's safe to drop that folder directly in the source folder of your own project.

License
-------------
This code is available under the terms of the Mozilla Public License v2.0 http://mozilla.org/MPL/2.0/

To-Do
-------------
* Implement a Generic B-Sline type that supports arbitrary powers, in addition to the cubic-only version. The generic one would almost certainly have worse performance and numerical stability than the cubic-only version, so it's worth keeping both.
* Add support for arbitrary T value differences in the Cubic B-Spline
* Integrate a spatial index library to replace the sweep-and-prune algorithm currently used by the SplineInverter

