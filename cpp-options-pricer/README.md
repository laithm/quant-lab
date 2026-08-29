# C++ Options Pricer

A compact **C++20 derivatives-pricing project** built around one idea: implement the same vanilla option valuation several ways, then verify that the methods agree for the right reasons.

The project includes:

- Black–Scholes closed-form pricing for European calls and puts
- analytic Delta, Gamma, Vega, Rho and Theta
- Cox–Ross–Rubinstein binomial trees for European and American options
- terminal-value GBM Monte Carlo with antithetic variates
- Monte Carlo standard-error reporting
- finite-difference verification of analytic Greeks
- deterministic validation tests and a small results-export harness

The point is not to produce a single attractive price. It is to make the numerical behaviour **measurable and testable**.

## Validation

The test suite checks that:

- textbook Black–Scholes call/put values are reproduced;
- put–call parity holds to numerical tolerance;
- analytic Greeks agree with bumped finite differences;
- a CRR tree converges toward Black–Scholes as the number of steps increases;
- an American put is never worth less than its European equivalent;
- the Monte Carlo estimate lands within three reported standard errors of the Black–Scholes reference value.

## Build and test

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build
ctest --test-dir build --output-on-failure
```

Run the comparison harness:

```bash
mkdir -p output
./build/pricer_run
```

The harness compares CRR convergence and Monte Carlo estimates against the Black–Scholes reference, prints analytic versus finite-difference Greeks, and writes `output/results.json`.

## Layout

```text
include/pricer/
  payoff.hpp          option specification + terminal payoff
  black_scholes.hpp   closed-form price + analytic Greeks
  binomial.hpp        CRR tree, European + American exercise
  monte_carlo.hpp     GBM Monte Carlo + antithetic variates + SE
src/
  main.cpp            comparison / validation harness
tests/
  test_pricer.cpp     numerical and financial invariants
```

## Scope

This is deliberately a small, inspectable research/engineering project rather than a trading platform. Current scope is vanilla equity-style options under standard Black–Scholes/GBM assumptions; calibration, volatility surfaces, rates curves and production market-data/execution infrastructure are outside the project.

## Why C++

I’m using the project to combine derivatives mathematics with performance-oriented software engineering: explicit numerical methods, deterministic tests, reproducible builds and a codebase small enough to reason about end-to-end.
