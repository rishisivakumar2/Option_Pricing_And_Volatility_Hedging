# Option Pricing and Volatility Hedging

A Python research project exploring European option pricing, volatility, and dynamic hedging. The first milestone is a validated analytical Black–Scholes pricing engine.

## Status

Planning stage. This repository currently contains the project outline only. Pricing code, dependencies, tests, and automated workflows have not been implemented.

## Research direction

How does discrete delta-hedging P&L change when realized volatility differs from implied volatility, and how do hedge frequency and transaction costs affect the result?

The Black–Scholes engine will provide the reference prices and Greeks for these later experiments.

## First milestone: Black–Scholes engine

- European call and put prices, including a continuous dividend yield.
- Analytical delta, gamma, theta, vega, and rho.
- Documented units, model assumptions, input validation, and limiting cases.
- Scalar inputs first, then NumPy array support.
- Mathematical validation and an explanatory notebook.

Here, “solver” means evaluation of the analytical pricing formulas. Implied-volatility inversion and a numerical PDE solver are separate extensions.

## Proposed tools

Python, NumPy, SciPy, pytest, Matplotlib, and Jupyter. Implement the pricing and Greek formulas directly, using SciPy for the normal distribution functions. Choose compatible versions and record dependencies when implementation begins.

## Planned structure

```text
src/options_lab/
    __init__.py
    black_scholes.py
    greeks.py
tests/
    test_black_scholes.py
    test_greeks.py
notebooks/
    01_black_scholes_validation.ipynb
examples/
    price_option.py
figures/
.github/workflows/
    tests.yml
pyproject.toml
README.md
docs/
    ROADMAP.md
    MODEL_SPEC.md
```

This is a proposed structure, not a list of implemented files. Reusable calculations belong in the package; notebooks import the package and explain experiments.

## Milestone completion criteria

1. Prices reproduce independently established benchmark values.
2. Put–call parity, discounted bounds, expiry payoffs, and zero-volatility limits pass validation.
3. Analytical Greeks agree with finite differences away from singularities.
4. Array results match repeated scalar evaluations.
5. A fresh checkout can install the package, run tests, and reproduce the validation notebook.
6. The README includes a working example, assumptions, conventions, and plots.

Only after these criteria are met should the first release be tagged `v0.1.0`.

## Project documents

- [Roadmap and implementation checklist](docs/ROADMAP.md)
- [Model conventions and validation specification](docs/MODEL_SPEC.md)

## Repository workflow

Use `main` for completed milestones and short feature branches for changes. Add automated Python testing with GitHub Actions when executable code and tests exist. Select a license before inviting reuse of the project.

## Later milestones

Black–Scholes and Greeks → implied-volatility inversion → Monte Carlo pricing → discrete delta hedging → realized versus implied volatility → transaction costs.
