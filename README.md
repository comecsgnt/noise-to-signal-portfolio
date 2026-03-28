# From Noise to Signal: Portfolio Strategies with Covariance Filtering

**Côme Genet, Paul Beaumont, Antoine Mazet**

Course: *Portfolio Allocation* — Christian Bongiorno & Romain Perchet

---

## Overview

This project investigates the out-of-sample performance of various portfolio strategies on a large cross-section of US equities, combining two modules from the course:

- **Module 1 (Optimization)**: Global Minimum Variance, Robust Optimization (Scherer type)
- **Module 2 (Covariance Cleaning)**: Marchenko–Pastur / RMT eigenvalue clipping, Ledoit–Wolf shrinkage, EWMA, neural network end-to-end cleaning

All strategies are evaluated in a **walk-forward backtest** with realistic transaction costs (5 bps) and no look-ahead bias.

---

## Key results

| Strategy | Sharpe | AnnVol | MaxDD | AvgTO |
|----------|--------|--------|-------|-------|
| GMV-CLIP | 3.01 | 9.4% | -13.2% | 0.197 |
| GMV-LW | 3.01 | 7.4% | -10.1% | 0.262 |
| RO-CLIP | 1.98 | 19.1% | -19.0% | 0.507 |
| RO-EWMA | 1.95 | 13.0% | -17.0% | 0.713 |
| NN-GMV | 1.43 | 5.3% | -5.1% | 0.075 |
| GMV-EWMA | 0.61 | 26.7% | -42.2% | 6.717 |
| GMV-MLE | 0.40 | 31.5% | -53.3% | 7.490 |

**Main finding**: covariance regularization (LW, RMT clipping) is the first-order driver of performance. Robust Optimization adds raw return but at the cost of higher risk and turnover, without improving the Sharpe ratio once the covariance is well-regularized.

---

## Notebook structure

| Section | Content |
|---------|---------|
| 0 | Imports & global parameters |
| 1 | Data loading & preprocessing |
| 2 | Eigenvalue analysis (Marchenko–Pastur bounds) |
| 3 | Covariance estimators (MLE, LW, CLIP, EWMA) |
| 4 | GMV walk-forward backtest |
| 5 | Robust Optimization: kappa sensitivity + GMV vs RO ablation |
| 6 | Neural Network GMV (biLSTM eigenvalue cleaning) + ablation |
| 7 | Full strategy comparison |
| 8 | Stress test: 2008 financial crisis |

---

## Requirements

```bash
pip install numpy pandas torch scikit-learn scipy matplotlib seaborn tqdm
```

Tested with Python 3.11. No GPU required.

---

## Data

The notebook uses the **Wiki Prices** dataset (`wiki_prices.csv`), a collection of daily adjusted close prices for US equities available on [Quandl/Nasdaq Data Link](https://data.nasdaq.com/databases/WIKIP).

Place `wiki_prices.csv` in the same directory as the notebook before running. The file should contain at minimum three columns: `date`, `ticker`, `adj_close`.

The notebook automatically:
1. Filters to dates from 2000-01-01 onward
2. Randomly selects 500 tickers (seed 42) to avoid look-ahead bias
3. Saves a preprocessed `returns_window.csv` (150 assets, ~1026 daily returns)

---

## Backtest parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| `WINDOW_IN` | 126 | Estimation window for covariance (~6 months) |
| `REBALANCE_STEP` | 10 | Rebalancing frequency (trading days) |
| `COST_BPS` | 5.0 | Proportional transaction cost (basis points) |
| `N_ASSETS` | 500 | Number of stocks randomly selected |
| `WINDOW_LENGTH` | 1000 | In-sample period length (trading days) |
| `RANDOM_SEED` | 42 | Seed for reproducible ticker selection |

---

## How to run

```bash
git clone https://github.com/<your-username>/portfolio-allocation.git
cd portfolio-allocation

# Place wiki_prices.csv in this directory, then:
jupyter notebook Portfolio_Allocation_Final.ipynb
```

Run cells sequentially. Section 1 generates `returns_window.csv` on first run. Sections 5 (RO ablation) and 6 (NN training, 50 epochs) are the most compute-intensive, taking approximately 3–5 minutes each on CPU.

---

## Reproducibility

All random operations use `RANDOM_SEED = 42` via `np.random.seed(42)` and `torch.manual_seed(42)`. Results may vary slightly across platforms due to floating-point differences in `scipy.optimize.minimize` (used for RO) and `torch.linalg.eigh`.
