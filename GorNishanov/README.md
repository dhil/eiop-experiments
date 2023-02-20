# Gor Nishanov's CppCon'18 demo

This directory contains a slightly modified copy of [Gor Nishanov's
CppCon'18 demo
files](https://github.com/GorNishanov/await/tree/master/2018_CppCon/src). The following changes were made:

* Replace all uses of `#pragram once` with explicit header guards.
* Use `clang++-17` as the compiler (i.e. `CXX=clang++-17`)
  - Drop `-fcoroutines-ts` flag
  - Replace `-std=c++2a` by `-std=c++20`
* Drop all `experimental` annotations.
* Add a `clean` rule to the makefile.