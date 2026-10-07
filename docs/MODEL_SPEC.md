# Black–Scholes model specification

## Scope and assumptions

European calls and puts under constant volatility, a constant continuously compounded risk-free rate, and a constant continuous dividend yield. The underlying follows geometric Brownian motion. The model assumes frictionless markets and continuous trading. American exercise and discrete cash dividends are outside the first milestone.

## Inputs

| Symbol | Meaning | Convention |
| --- | --- | --- |
| S | Current underlying price | Positive, finite |
| K | Strike | Positive, finite, same currency as S |
| T | Remaining time to expiry | Nonnegative, finite, years |
| r | Risk-free rate | Finite annual continuously compounded decimal; negative values allowed |
| sigma | Volatility | Nonnegative, finite, annualized decimal |
| q | Dividend yield | Finite annual continuous decimal; default zero |
| option_type | Payoff type | Explicit call or put |

Rates and volatility use decimals: 0.20 denotes 20%. No calendar-date or day-count conversion is required in the first version; the caller supplies T in years.

## Outputs and Greek conventions

- Price is per underlying unit. Apply an option contract multiplier separately.
- Delta is the first derivative with respect to S.
- Gamma is the second derivative with respect to S.
- Theta is the calendar-time derivative, equal to minus the derivative with respect to remaining maturity T, with other inputs fixed. Report per year.
- Vega is the derivative with respect to sigma, per unit change. Divide by 100 for a one-percentage-point change.
- Rho is the derivative with respect to r, per unit change. Divide by 100 for a one-percentage-point change.

## Analytical formulas for positive T and sigma

Let N denote the standard normal cumulative distribution function.

```text
d1 = [ln(S/K) + (r - q + sigma²/2) T] / (sigma sqrt(T))
d2 = d1 - sigma sqrt(T)

Call = S exp(-qT) N(d1) - K exp(-rT) N(d2)
Put  = K exp(-rT) N(-d2) - S exp(-qT) N(-d1)
```

## Boundary policies to implement

At T = 0, return intrinsic payoff. At sigma = 0 and T > 0, return the deterministic discounted payoff:

```text
Call = max(S exp(-qT) - K exp(-rT), 0)
Put  = max(K exp(-rT) - S exp(-qT), 0)
```

Define and document Greek behavior separately at these boundaries. Do not silently assign ordinary derivatives at nondifferentiable payoff kinks. Decide whether undefined outputs produce a documented error or an explicitly marked missing value before implementation.

Reject invalid option types, negative T or sigma, nonpositive S or K, and nonfinite inputs with clear errors. Specify array broadcasting and invalid-element behavior before adding array support.

## Validation requirements

Put–call parity:

```text
Call - Put = S exp(-qT) - K exp(-rT)
```

Discounted European bounds:

```text
max(S exp(-qT) - K exp(-rT), 0) <= Call <= S exp(-qT)
max(K exp(-rT) - S exp(-qT), 0) <= Put  <= K exp(-rT)
```

Compare analytical Greeks with finite differences at smooth interior points. For theta, account for the sign difference between calendar time and remaining maturity. Use multiple step sizes to distinguish truncation error from floating-point cancellation.

Test ordinary parameter combinations and difficult regions. For small option values, use absolute tolerances alongside relative tolerances. Reference prices must be established independently of the implementation under test.

## Initial demonstration inputs

S = 100, K = 100, T = 1 year, r = 0.04, sigma = 0.20, q = 0. Compute benchmark results during implementation and verify them independently before recording expected values.
