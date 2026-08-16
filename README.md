# Deep Reinforcement Learning for Portfolio Optimization

A replication and evaluation of the **TD3-based portfolio selection framework** proposed by Jiang, Olmo & Atwi (2024), using S&P 100 stock data.

This was a team project completed at the Technical University of Munich. Our goal was to understand a relatively complex deep reinforcement learning approach by reproducing its main ideas in practice, and then exploring how the model behaved under different network architectures, benchmark strategies, transaction costs, and risk-aversion settings.

For detailed methodology, model architecture, benchmark comparisons, sensitivity analysis, and result visualizations, please refer to the presentation slides and project report:

📊 `DRL_portfolio_management_final[1].pptx`

📄 `DRL_Report_Final1.pdf

---

## 1. Project Overview

Portfolio management is a sequential decision-making problem: an investor observes the market, decides how to allocate capital across assets, and continuously adjusts the portfolio as market conditions change.

In this project, we replicated the main framework proposed by **Jiang, Olmo & Atwi (2024)**, which applies the **Twin Delayed Deep Deterministic Policy Gradient (TD3)** algorithm to portfolio selection while considering both transaction costs and investor risk aversion.

Our implementation focused on:

- Reproducing the main TD3 portfolio-selection framework
- Comparing MLP and LSTM network architectures
- Comparing TD3 with traditional portfolio strategies
- Testing different transaction-cost and risk-aversion settings

---

## 2. Data

We used historical closing-price data from **S&P 100 stocks** covering the period from 2010 to 2023.

After data cleaning, **95 stocks** were retained for the analysis.

Asset prices were transformed into relative price changes to reduce the influence of differences in absolute price levels.

---

## 3. Portfolio Environment

Following the framework of the paper, we formulated portfolio selection as a reinforcement learning problem.

### State

The state includes:

- Normalized current asset prices
- Portfolio weights from the previous time step

### Action

The TD3 agent operates in a continuous action space and determines how the portfolio allocation should be adjusted across assets.

### Reward

The reward considers three components:

```text
Reward
   =
Portfolio Return
   -
Transaction Cost
   -
Risk-Aversion Penalty
```

This allows the model to consider not only portfolio returns, but also the costs of rebalancing and the investor's tolerance for risk.

---

## 4. TD3 Implementation

We implemented **Twin Delayed Deep Deterministic Policy Gradient (TD3)** as the main reinforcement learning algorithm.

TD3 uses an actor-critic architecture designed for continuous action spaces, making it suitable for portfolio allocation decisions.

We implemented and compared two network architectures:

- **TD3-MLP**
- **TD3-LSTM**

We also experimented with training parameters such as the learning rate and number of episodes to improve training stability.

In our experiments, the **TD3-MLP** version performed better than TD3-LSTM and was therefore used for the subsequent comparisons.

---

## 5. Benchmark Comparison

We compared TD3-MLP with two traditional portfolio strategies:

- Minimum Variance Portfolio
- Maximum Sharpe Ratio Portfolio

Performance was evaluated using:

- Cumulative Return
- Annualized Return
- Annual Volatility
- Sharpe Ratio
- Maximum Drawdown
- Calmar Ratio

### Main Results

| Strategy | Cumulative Return | Annualized Return | Sharpe Ratio |
|---|---:|---:|---:|
| TD3-MLP | **37%** | **13%** | **0.69** |
| Minimum Variance | 24% | 9% | 0.58 |
| Maximum Sharpe | 7% | 3% | 0.15 |

Within our experimental setting, TD3-MLP achieved higher cumulative returns and Sharpe ratios than both traditional benchmark strategies.

---

## 6. Sensitivity Analysis

We also tested how the TD3-MLP model behaved under different assumptions.

### Transaction Costs

We increased the transaction-cost parameter while keeping the risk-aversion parameter constant.

Higher transaction costs reduced trading activity and were associated with lower portfolio returns.

### Risk Aversion

We also varied the risk-aversion parameter while keeping transaction costs constant.

As risk aversion increased, the model became more conservative and portfolio returns declined.

These experiments helped us understand how strongly the behavior of a reinforcement learning portfolio model can depend on the assumptions built into its reward function.

---

## 7. What I Learned

This was one of the more challenging projects for me because deep reinforcement learning was quite new to us.

Replicating an existing paper made the topic much more concrete. Instead of only learning TD3 theoretically, we had to understand how the state, action, reward function, actor-critic networks, and training process actually fit together in a portfolio problem.

I also found it interesting to see how sensitive the final results were to choices such as the network architecture, training parameters, transaction costs, and risk aversion.

---

## 8. Technologies & Methods

- Python
- Deep Reinforcement Learning
- TD3
- Actor-Critic Networks
- MLP
- LSTM
- Portfolio Optimization
- Model Evaluation
- Sensitivity Analysis

---

## Reference

Jiang, Y., Olmo, J., & Atwi, M. (2024). *Deep reinforcement learning for portfolio selection*. Global Finance Journal, 62, 101016.
