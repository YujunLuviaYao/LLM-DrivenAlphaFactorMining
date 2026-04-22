# LLM-Driven Alpha Factor Mining

Final project for DSGA-1019 (Advanced Python for Data Science).

---

## 1. Project Structure

```text
LLM-DrivenAlphaFactorMining/
├── data/
│   ├── sp500_tickers.csv
│   └── sp500_cache.pkl
├── notebooks/
│   ├── baseline.ipynb
│   ├── generate_1000.ipynb
│   ├── evolve_factors.ipynb
│   ├── opt1.ipynb
│   ├── opt2.ipynb
│   ├── opt3v.ipynb
│   ├── opt4.ipynb
│   ├── opt5.ipynb
│   ├── opt6.ipynb
│   └── opt6_full.ipynb
├── results/
│   ├── evaluation/
│   ├── timing/
│   └── plots/
├── reports/
└── README.md
```

---

## 2. Dependencies

Python 3.10+ recommended.

```bash
pip install numpy pandas scipy matplotlib yfinance anthropic tqdm bottleneck numba jupyter line_profiler
```

---

## 3. Notebook Run Order

1. `notebooks/baseline.ipynb`
2. `notebooks/opt1.ipynb`
3. `notebooks/opt2.ipynb`
4. `notebooks/opt3v.ipynb`
5. `notebooks/opt4.ipynb`
6. `notebooks/opt5.ipynb`
7. `notebooks/opt6.ipynb`
8. `notebooks/opt6_full.ipynb`

---

## 4. Optional Notebook

- `notebooks/generate_1000.ipynb`: generate a larger factor pool (about 1000 factors) for broader search/experiments.
- `notebooks/evolve_factors.ipynb`: evolve/filter existing factors using complexity constraints and backtest performance.

These are optional and not required for the main Baseline -> Opt6 reproduction order.

---

## 5. Where to Check Results

Evaluation output:
- `results/evaluation/factor_evaluation.csv`

Timing outputs:
- `results/timing/baseline_timing.csv`
- `results/timing/opt1_timing.csv`
- `results/timing/opt2_timing.csv`
- `results/timing/opt3_timing.csv`
- `results/timing/opt4_timing.csv`
- `results/timing/opt5_timing.csv`
- `results/timing/opt6_timing.csv`
- `results/timing/opt6_full_timing.csv`
- `results/timing/final_submission_summary.csv`

Report:
- `reports/README_FINAL_EXPERIMENT.md`
