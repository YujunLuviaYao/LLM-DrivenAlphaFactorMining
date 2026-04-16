<<<<<<< HEAD
# LLM-DrivenAlphaFactorMining
Final project for DSGA-1019 (Advanced Python for Data Science), focused on optimizing the backtesting of alpha factors generated via the Anthropic Claude API.
=======
# LLM Alpha Mining Pipeline

The project has been organized into a layered structure of "code / results / reports" for easier development and direct reporting.

## 1. Project Structure

```text
project/
├── README.md
├── data/                          # raw and cached data
│   ├── sp500_tickers.csv
│   └── sp500_cache.pkl
├── notebooks/                     # main experiment entry notebooks
│   ├── baseline.ipynb
│   ├── opt1.ipynb
│   ├── opt2.ipynb
│   ├── opt3.ipynb
│   └── opt4_colab.ipynb           # GPU version (recommended on Colab)
├── results/
│   ├── evaluation/                # factors and evaluation outputs
│   │   ├── factors.json
│   │   └── factor_evaluation.csv
│   ├── timing/                    # performance timing outputs
│   │   ├── opt1_timing.csv
│   │   ├── opt2_timing.csv
│   │   ├── opt3_timing.csv
│   │   ├── opt3_timing_tuned.csv
│   │   ├── opt3_thread_sweep.csv
│   │   ├── opt3_best_thread.csv
│   │   ├── baseline_opt1_runs.csv
│   │   ├── baseline_opt1_summary.csv
│   │   ├── baseline_opt1_opt2_summary.csv
│   │   ├── baseline_opt1_opt2_opt3_summary.csv
│   │   └── baseline_opt1_opt2_opt3_tuned_summary.csv
│   └── plots/                     # visualization plots
│       ├── plot1_ranking.png
│       ├── plot2_scatter.png
│       └── plot3_top_factor.png
├── reports/
│   └── README_OPT1_EXPERIMENT.md  # Baseline/Opt1/Opt2 experiment report
└── docs/
    └── LLM_Alpha_Mining_Proposal.pptx
```

Notes:

- The project root keeps symlinks for `factors.json` and `factor_evaluation.csv` to remain compatible with existing notebook paths.

## 2. Quick Start

Python 3.10+ is recommended. Install dependencies first:

```bash
pip install numpy pandas scipy matplotlib yfinance google-generativeai jupyter line_profiler
```

Recommended execution order:

1. `notebooks/baseline.ipynb`
2. `notebooks/opt1.ipynb`
3. `notebooks/opt2.ipynb`
4. `notebooks/opt3.ipynb`
5. `notebooks/opt4_colab.ipynb`(Colab GPU)

Performance results:

- `results/timing/baseline_opt1_opt2_opt3_tuned_summary.csv`

Experiment reports:

- `reports/README_OPT1_EXPERIMENT.md`

## 3. Pipeline Overview

1. Data Loading：Read `data/sp500_cache.pkl` or download and cache it
2. Factor Generation：Generate/load factor expressions (`factors.json`)
3. Backtesting：Compute factor matrices
4. Evaluation：Compute IC/ICIR/Sharpe/MDD/Turnover
5. Visualization：Generate ranking/scatter/Top-factor plots

## 4. Current Stage

- `baseline.ipynb`: baseline version
- `opt1.ipynb`: Python best-practices optimization
- `opt2.ipynb`: NumPy vectorization optimization
- `opt3.ipynb`: Numba JIT optimization (core kernels use `@njit(parallel=True)`)
- `opt4_colab.ipynb`: GPU acceleration (CuPy + optional Numba CUDA)
>>>>>>> 1de6795 (first commit)
