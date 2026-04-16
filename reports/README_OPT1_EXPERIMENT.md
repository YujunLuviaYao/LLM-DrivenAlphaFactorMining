# Backtesting Acceleration Experiment Report (Baseline / Opt1 / Opt2 / Opt3 Tuned)

## 1. Experiment Objective

Validate whether the staged optimization strategy is effective:

1. `Opt1` (Python best practices)
2. `Opt2` (NumPy vectorization)
3. `Opt3` (Numba JIT + parallel tuning)

## 2. Experiment Setup

- Data: `data/sp500_cache.pkl`
- Factors: first 20 factors from `results/evaluation/factors.json`
- Sample size: 752 days × 483 stocks
- Metric: total runtime of `compute_all_factors` (seconds)
- Notebooks:
  - Baseline: `notebooks/baseline.ipynb`
  - Opt1: `notebooks/opt1.ipynb`
  - Opt2: `notebooks/opt2.ipynb`
  - Opt3: `notebooks/opt3.ipynb` (with thread sweep)

## 3. Result Summary

Result files:

- `results/timing/opt1_timing.csv`
- `results/timing/opt2_timing.csv`
- `results/timing/opt3_timing_tuned.csv`
- `results/timing/opt3_thread_sweep.csv`
- `results/timing/opt3_best_thread.csv`
- `results/timing/final_submission_summary.csv`

Current comparison:

| Method | Runtime(s) | Speedup vs Baseline | Improvement vs Baseline | Speedup vs Opt1 | Speedup vs Opt2 | Threads |
|---|---:|---:|---:|---:|---:|---:|
| Baseline | 2.5790 | 1.000x | 0.00% | 0.769x | 0.294x | - |
| Opt1 | 1.9844 | 1.300x | 23.06% | 1.000x | 0.382x | - |
| Opt2 | 0.7575 | 3.405x | 70.63% | 2.620x | 1.000x | - |
| Opt3 Tuned | 0.1178 | **21.889x** | **95.43%** | **16.843x** | **6.429x** | 8 |

## 4. Why It Improved

### 4.1 Opt1 (Python best practices)

- Cached `eval / ctx / builtins`
- Precompiled expressions with `compile(...)`
- Replaced per-column Python loop in `ts_corr` with `rolling().corr()`

### 4.2 Opt2 (NumPy vectorization)

- Moved core operators to `ndarray` (`ts_mean/std/delta/corr`, `rank`, `zscore`)
- Used vectorized and cumulative-sum computations to reduce Pandas overhead

### 4.3 Opt3 (Numba JIT + parallel tuning)

- Added `@njit(parallel=True)` + `prange` to core kernels
- Performed thread sweep (`1/2/4/8`) and selected the best configuration
- Best thread count in this project: `8`

## 5. line_profiler Suggestions

Focus on:

1. Baseline: `compute_all_factors -> compute_factor -> ts_corr`
2. Opt1: `compute_all_factors -> ts_corr`
3. Opt2: `compute_all_factors -> rolling_corr_np / rank_rows_np`
4. Opt3: `compute_all_factors -> rolling_corr_nb / rank_rows_nb`

Key checks:

- `Total time`
- Whether hotspots move from Python layer to JIT kernels

## 6. Thread Sweep Result

- 8 threads: 0.0851s (best)
- 4 threads: 0.0974s
- 2 threads: 0.1554s
- 1 thread: 0.3085s

## 7. Scope Note

Baseline uses historical aggregated statistics, while Opt1/Opt2/Opt3 use the latest notebook runs in this project.

## 8. Opt4 (Colab GPU) Note

From `results/timing/opt4_timing.csv`, Opt4 is 1.0265s in Colab GPU. It is faster than Baseline/Opt1, but slower than Opt2/Opt3 in the current measurement scope.
