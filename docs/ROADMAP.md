# Project roadmap

## Milestone 0 — Repository and specification

- [x] Draft the README and project scope.
- [x] Define model conventions and validation requirements.
- [x] Create the GitHub repository `Option_Pricing_And_Volatility_Hedging`.
- [x] Publish the initial project documentation.
- [x] Choose Python 3.12 with pip, a local virtual environment, and `pyproject.toml` dependency declarations.
- [x] Create the installable `src/options_lab` package skeleton and a local development environment.

Milestone 0 is complete. The package installs and imports, and exact development dependency versions are recorded in `requirements-dev.lock.txt`. Setup instructions are in the README. The pricing modules contain documentation placeholders; all pricing functionality remains in Milestone 1.

## Milestone 1 — Analytical Black–Scholes engine

### 1. Pricing

- [ ] Implement scalar European call and put pricing with dividend yield.
- [ ] Validate inputs and define expiry and zero-volatility behavior.
- [ ] Establish independently verified reference examples.
- [ ] Test put–call parity, discounted price bounds, and monotonicity.

### 2. Greeks

- [ ] Implement delta, gamma, theta, vega, and rho.
- [ ] Document units and theta sign convention.
- [ ] Define behavior at payoff kinks and other singular boundaries.
- [ ] Compare Greeks with finite differences over several step sizes.

### 3. Arrays and numerical behavior

- [ ] Define supported shapes and broadcasting behavior.
- [ ] Add NumPy array support and verify scalar consistency.
- [ ] Check deep in/out-of-the-money cases, short maturities, low volatility, dividends, and negative rates.
- [ ] Set justified absolute and relative tolerances.

### 4. Demonstration and release

- [ ] Create a validation notebook with benchmark tables and plots.
- [ ] Plot call and put prices, delta, and gamma against spot.
- [ ] Explain analytical versus numerical Greek comparisons.
- [ ] Add installation, example usage, and test instructions.
- [ ] Configure automated tests for pushes and pull requests.
- [ ] Verify reproduction from a fresh checkout.
- [ ] Tag `v0.1.0` only after validation is complete.

## Milestone 2 — Implied volatility

Invert the pricing function using a bracketed method and Newton–Raphson. Investigate low-vega failure cases, admissible price bounds, convergence, and recovery of known synthetic volatilities.

## Milestone 3 — Monte Carlo

Simulate risk-neutral geometric Brownian motion, estimate discounted European option payoffs, and compare estimates and confidence intervals with analytical prices. Study convergence over repeated seeded experiments.

## Milestone 4 — Discrete delta hedging

Simulate stock paths, rebalance delta at discrete dates, and track a consistently defined self-financing cash account. Study terminal hedging-error distributions and convergence with hedge frequency.

## Milestone 5 — Volatility mismatch

Vary actual volatility while holding pricing volatility fixed. Compare hedging with implied volatility and with the assumed actual volatility. Explain the assumptions under which theoretical predictions apply.

## Milestone 6 — Transaction costs and project report

Add proportional trading costs and investigate the tradeoff between frequent hedging and trading expense. Produce reproducible figures and a concise report answering the central research question.

## Optional extensions

Market-data volatility surfaces, binomial trees, numerical PDE methods, American options, and volatility forecasting. Prioritize these only after the core pricing and hedging investigation is complete.

## Suggested GitHub issue titles

1. Define package environment and installation (completed in Milestone 0)
2. Implement European call and put pricing
3. Validate pricing identities and boundary cases
4. Implement and validate analytical Greeks
5. Add array support and numerical stress cases
6. Build the Black–Scholes validation notebook
7. Add automated testing and prepare v0.1.0

These titles are a proposed backlog; GitHub issues have not yet been created.
