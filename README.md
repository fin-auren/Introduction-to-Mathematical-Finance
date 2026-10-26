# Introduction-to-Mathematical-Finance



This notebook provides a structured review of the core disciplines supporting modern quantitative finance, including historical contexts, mathematical foundations, and financial applications.

---

## 1. Introduction to Mathematical Finance
* **Evolution**: Quantitative finance is a relatively new field (~30 years old) transitioning from intuitive/clerical trading to highly quantitative strategies powered by mathematics, physics, and computer science.
* **Financial Markets**: Serves as platforms for capital allocation, risk transfer, and investment across exchanges, ECNs, and OTC markets.
* **Products & Institutions**: Explores primary asset classes (equities, debt, commodities, real estate, and derivatives) and key participants (investment/commercial banks, asset managers, hedge funds, PE firms, and governments).
* **Greeks**: Sensitivities used to manage option portfolios:
  * **Delta**: Sensitivity to underlying price changes.
  * **Gamma**: Curvature/convexity (rate of change of Delta).
  * **Theta**: Time decay.
  * **Vega** (colloquially "Kappa"): Sensitivity to volatility.
* **Risk & Trading**: Discusses concepts like Leverage, Value at Risk (VaR), and diverse trading strategies (Directional, Arbitrage, Systematic/Stat Arb, Relative Value).

## 2. Linear Algebra Foundations
* **Matrices**: Looked at both as static datasets (e.g., historical stock prices) and as linear transformations ($A: \mathbb{R}^n \rightarrow \mathbb{R}^m$).
* **Eigenvalue Decomposition ($Av = \lambda v$)**: Reveals invariant directions (eigenvectors) along which the transformation only scales (eigenvalues). Applicable only to square, diagonalizable matrices.
* **Singular Value Decomposition ($A = U\Sigma V^T$)**: Generalizes diagonalization to *any* rectangular/square matrix, enabling reduced-order representation, data compression, and factor extraction for asset returns.
* **Perron-Frobenius Theorem**: Guarantees that a square, positive matrix has a unique, strictly positive dominant eigenvalue ($\lambda_0$) with a positive eigenvector, with wide applications in Markov chains and network analysis.

## 3. Probability Theory Review
* **Random Variables**: Formulated through PMFs (discrete) and PDFs (continuous), highlighting expectations, variances, and joint independence.
* **Asset Distributions**: Evaluates why the Log-Normal distribution is superior to the Normal distribution for modeling absolute stock prices (preventing negative prices and focusing on percentage/logarithmic returns).
* **Moment Generating Functions (MGFs)**: $M_X(t) = E[e^{tX}]$ uniquely identifies probability distributions, generates analytical moments through derivatives ($M_X^{(k)}(0) = E[X^k]$), and aids in convergence proofs.
* **Asymptotic Theorems**:
  * **Law of Large Numbers (LLN)**: Sample averages converge in probability to the true expected value ($\bar{X}_n \to \mu$).
  * **Central Limit Theorem (CLT)**: Normalized sum of IID random variables converges in distribution to a normal distribution ($N(0, \sigma^2)$), regardless of the parent distribution.

## 4. Stochastic Processes, Random Walks & Martingales
* **Simple Random Walk**: A fundamental discrete-time process with independent and stationary increments, characterized by $\text{Std}(X_t) = \sqrt{t}$ and a recurrence property (infinite returns to origin).
* **Markov Chains**: Memoryless processes where the future state depends only on the current state. Transition probabilities are calculated via powers of the transition matrix ($A^n$), converging under Perron-Frobenius conditions to a stationary distribution ($Av = v$).
* **Martingales**: Models of fair games where $E[X_{t+1} \mid X_0, \dots, X_t] = X_t$. 
* **Optional Stopping Theorem**: States that the expected value of a stopped martingale remains its initial expectation ($E[X_\tau] = E[X_0]$) under a bounded stopping time $\tau$. This elegant tool easily solves problems like the *Gambler's Ruin*.

## 5. Multiple Linear Regression (MLR) in Finance
Regression analysis serves as the statistical backbone for empirical finance. Main use cases include:
1. **Stock Return Prediction**: Modeling future returns using factors like P/E ratios, market cap, and momentum.
2. **Asset Pricing Models**: Testing economic theories such as the **CAPM** ($R_i - R_f = \alpha + \beta(R_m - R_f) + \epsilon$) and Multi-Factor Models (Fama-French, Carhart).
3. **Portfolio Risk & Performance Attribution**: Attributing returns to specific factor exposures (value, size, momentum) and evaluating active manager skill ($\alpha$).
4. **Credit Risk & Macroeconomic Forecasting**: Estimating default probabilities for loans and projecting GDP growth, inflation, and bond yields.

# Present Value

Fixed interest rate `i`Definition with `def` function `D(c1)`This function returns the present value with `return` statement

```python
i = 0.1

def D(c1):
  return c1/(1+i)

print(D(12.1)) # Output: 10.999999999999998
print(D(11))   # Output: 10.0
```

# Net Present Value
The net present value is the sum of the cash outflow today and the present value of the cash inflow in one year.

```python
def NPV(c):
  return c[0] + D(c[1])

cA = (-10.5, 12.1)
cB = (-10.5, 11)

print(NPV(cA)) # Output: 0.4999999999999982
print(NPV(cB)) # Output: -0.5
```

```python
import numpy as np
c0 = -10 
c1 = np.array((20,5))

# Scalar multiplication and vector addition
print(1.5 * c1 + 2)
print(c1 + 1.5 * np.array((10,4)))
```

# Financial Assets
Financial assets are financial instruments ("contracts") that have a fixed price today and an uncertain price in one year. Think of a share in the equity of a firm that conducts an investment project. Such a share might be available at a price today of S0. The price of the share in one year depends on the success of the investment project, i.e., whether a high cash inflow is observed in the state or a low one in the state.

```python
S0 = 10
S1 = np.array((12.5,7.5)) 
S = (S0, S1)

print(S[0])
print(S[1][0])
print(S[1][1])
```

# Risk
Risk in general refers to a situation in which a full probability distribution over future states of the economy is known.

```python
p = 0.4
P = np.array((p, 1-p))
```

# Expectation
The expectation can be interpreted as the weighted average, where the weights are given by the probabilities. It is an average since the probabilities add up to one.

```python
S1 = np.array((20,5))
np.dot(P, S1)
```

# Expected Return
The **expected return** of a financial asset is given as the expectation of the price in one year minus the price today.The **expected rate** of return then simply is the expected return divided by the price today.

```python
def ER(x0, x1):
  return np.dot(P, x1) - x0

def mu(x0, x1):
  return (np.dot(P, x1) - x0)/x0

def r(x0, x1):
  return (x1-x0)/x0

mu_val = np.dot(P, r(S0, S1))
```

# Variance and Volatility
```python
def sigma2(P, r, mu):
  return np.dot(P, (r-mu)**2)

def sigma(P, r, mu):
  return np.sqrt(np.dot(P, (r-mu)**2))
```

