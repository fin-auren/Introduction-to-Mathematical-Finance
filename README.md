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
