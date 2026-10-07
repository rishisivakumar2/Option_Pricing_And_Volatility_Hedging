# Option Pricing and Volatility Hedging

A Python research project exploring European option pricing, volatility, and dynamic hedging. The first milestone is a validated analytical Black–Scholes pricing engine.

## Status

Milestone 0 is complete: the repository has an installable package skeleton, a Python environment specification, and setup instructions. The pricing modules contain documentation placeholders only. Pricing functions, pricing tests, and automated workflows are planned for Milestone 1.

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

## Development environment

Use **Python 3.12** (a standard CPython installation), a project-local `.venv`, and pip. The Python minor version is recorded in `.python-version` and enforced in `pyproject.toml`. Python 3.12 receives security support through October 2028; see the [Python release information](https://blog.python.org/2026/10/python-31022-31117/).

NumPy and SciPy are runtime dependencies. The `dev` extra adds pytest, Matplotlib, JupyterLab, ipykernel, and the package build tool. Setuptools provides the build backend. Dependency ranges are maintained in `pyproject.toml`; `requirements-dev.lock.txt` records the exact versions verified on Windows with Python 3.12. Resolve and verify a new snapshot when upgrading dependencies. The snapshot is a version pin file, not a cross-platform hash lock.

Implement the pricing and Greek formulas directly in Milestone 1, using SciPy for the normal distribution functions.

## Get started on Windows

Install Python 3.12 if necessary, then run these commands in PowerShell:

```powershell
git clone https://github.com/rishisivakumar2/Option_Pricing_And_Volatility_Hedging.git
cd Option_Pricing_And_Volatility_Hedging
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements-dev.lock.txt
.\.venv\Scripts\python.exe -m pip install --no-build-isolation --no-deps -e .
.\.venv\Scripts\python.exe -c "import options_lab; print(options_lab.__file__)"
```

These commands use the virtual environment directly; PowerShell activation is optional. If your Python installation does not include the `py` launcher, use the path to your Python 3.12 executable for the environment creation command.

On macOS/Linux, create the environment with `python3.12 -m venv .venv` and use `.venv/bin/python` in place of `.\.venv\Scripts\python.exe` in subsequent commands. The pinned dependency snapshot was verified on Windows; other platforms may require a fresh dependency resolution.

For a fresh resolution of the declared dependency ranges instead of the snapshot:

```powershell
.\.venv\Scripts\python.exe -m pip install -e ".[dev]"
```

Launch notebooks with `.\.venv\Scripts\python.exe -m jupyterlab` from the repository root. Once pricing tests exist, run `.\.venv\Scripts\python.exe -m pytest`. At Milestone 0, no tests are collected.

## Current structure

```text
.python-version
.gitignore
pyproject.toml
requirements-dev.lock.txt
src/options_lab/
    __init__.py
    black_scholes.py
    greeks.py
tests/README.md
notebooks/README.md
examples/README.md
figures/README.md
README.md
docs/
    ROADMAP.md
    MODEL_SPEC.md
```

Reusable calculations belong in the package; notebooks import the package and explain experiments. Milestone 1 will add the validation notebook, executable examples, actual tests, and the automated testing workflow.

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
