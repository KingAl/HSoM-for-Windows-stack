# Haskell School of Music - Initial Setup for Windows

## Purpose

Getting package versions etc. correct for running Euterpea and associated packages on Windows
can be tricky. 
In particular, [Euterpea](https://www.euterpea.com/) has some specific recommendations for Haskell
version - the latest GHC (9+) is not expected to work with Euterpea on Windows, and instead
a version between 8.2.2 and 8.10.5 is recommended.

[Haskell Stack](https://docs.haskellstack.org/) 
allows us to build projects and run interactive `ghci` sessions under a specific
version of GHC and with specific versions of libraries installed, without it conflicting with
other library or GHC versions on your machine. That makes it a perfect for for working through
Haskell School of Music on Windows, where you have specific version requirements for this project
but may not want it to affect your GHC version and imports.

The `stack.yaml` and `stack.yaml.lock` in this repository record working compatible dependencies 
so that it's easier to get a working version up and running.

As at 2024-12-09, the referenced versions of 
[Euterpea](https://github.com/Euterpea/Euterpea2) (commit 55f7890, 2019-06-17)
  and [HSoM](https://github.com/Euterpea/HSoM) (commit 75338cb, 2017-06-01) 
 are the newest available, and the other dependencies are library versions that
 will work with them on Windows in my testing.

## Setup

If you haven't used Haskell or Stack before, ensure that Stack is installed on your machine per:

https://docs.haskellstack.org/

Create a directory where you'd like to work with Euterpea/HSoM and place the included yaml/yaml.lock into it.

Then see the [Euterpea](#euterpea) or [HSoM](#hsom-musical-gui) sections.
These will help you get the [examples](https://www.euterpea.com/examples/) from the Euterpea site running.

## Euterpea

From the command line, start a GHCI session with `stack ghci --package Euterpea` in your project directory.
stack will download the dependencies and build the package if it needs to.

Then per https://www.euterpea.com/examples/:

Run `import Euterpea`,
and finally, execute e.g. `play $ c 4 qn` to play a note.

## HSoM Musical GUI

### Installing GLUT
The Musical GUI uses GLUT (OpenGL Utility Toolkit) to display its Windows.
The original GLUT is no longer maintained, but lives on under the FreeGlut project.

FreeGlut Github: https://github.com/freeglut/freeglut/
FreeGlut Offical Site: https://freeglut.sourceforge.net/

If GLUT is not available, trying to use the HSoM graphical utilities will emit an error like:
`<interactive>: user error (unknown GLUT entry glutInit)`

The simplest thing to meet this requirement is to obtain "freeglut.dll" and put it in the path when using the project.
While it's possible to compile FreeGlut from source, per the official site binaries are downloadable
from here:
https://www.transmissionzero.co.uk/software/freeglut-devel/

Download a FreeGlut release from here, and extract freeglut.dll into your project directory.
Interactive sessions run in that directory will then see the dll and run successfully.
(Ensure you use the correct version of the DLL, e.g. x64 with a 64-bit release of Haskell etc.)

### Example Usage
First, Start a GHCI session with `stack ghci --package HSoM` to ensure the package is built.
Per the example site, run e.g. `import HSoM.Examples.MUIExamples2` then `bifurcate` to
open the "bifurcate" Musical GUI toy on-screen.