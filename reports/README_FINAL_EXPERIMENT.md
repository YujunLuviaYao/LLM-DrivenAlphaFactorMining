# LLM Alpha Mining Final Acceleration Report (Baseline ~ Opt4)

## 1. Reporting Scope

This report **does not rerun experiments**. All conclusions are compiled from existing historical timing CSV files.

- Report date: 2026-04-04
- Goal: provide unified results and conclusions for Baseline / Opt1 / Opt2 / Opt3 / Opt4

## 2. Data and Environment

- Data: `data/sp500_cache.pkl`
- Factors: first 20 factors from `results/evaluation/factors.json`
- Scale: 752 days × 483 stocks
- Metric: total runtime of `compute_all_factors` (seconds)

Notes:

- Baseline~Opt3 mainly come from local runs.
- Opt4 comes from Colab GPU runs.
- Because hardware differs, Opt4 comparisons are reference-only, not strict same-machine conclusions.

## 3. Result Files

- `results/timing/baseline_opt1_opt2_opt3_tuned_summary.csv`
- `results/timing/opt4_timing.csv`
- `results/timing/final_submission_summary.csv` (final summary used for submission)

## 4. Final Result Table

Source: `results/timing/final_submission_summary.csv`

| Method | Runtime(s) | Speedup vs Baseline | Improvement vs Baseline | Speedup vs Opt1 | Speedup vs Opt2 | Threads |
|---|---:|---:|---:|---:|---:|---:|
| Baseline | 2.5790 | 1.000x | 0.00% | 0.769x | 0.294x | - |
| Opt1 (Python best practices) | 1.9844 | 1.300x | 23.06% | 1.000x | 0.382x | - |
| Opt2 (NumPy vectorization) | 0.7575 | 3.405x | 70.63% | 2.620x | 1.000x | - |
| Opt3 Tuned (Numba + parallel) | 0.1178 | **21.889x** | **95.43%** | **16.843x** | **6.429x** | 8 |
| Opt4 (GPU/CuPy) | 1.0265 | 2.513x | 60.20% | 1.933x | 0.738x | - |

## 5. Conclusions

1. On the CPU path, `Opt3 Tuned` is currently the best solution with a clear speed advantage.
2. `Opt4` does not outperform `Opt2/Opt3` under this scope, mainly due to GPU startup cost, kernel granularity, expression scheduling, and data movement overhead.
3. For submission, the strongest main storyline is the continuous speedup path: Opt1 → Opt2 → Opt3; keep Opt4 as a GPU attempt and analysis section.

## 6. Ready-to-Use Paragraph

In this project, we implemented four optimization stages based on the proposal:

- Opt1: Python best practices
- Opt2: NumPy vectorization
- Opt3: Numba JIT parallelization (with thread sweep)
- Opt4: GPU acceleration (CuPy)

Based on historical timing CSV files, Baseline is 2.5790s; Opt1 is 1.9844s (+23.06%); Opt2 is 0.7575s (+70.63%); Opt3 (8 threads) is 0.1178s (+95.43%, 21.889x vs Baseline); Opt4 is 1.0265s and does not exceed Opt2/Opt3 in this environment.

Therefore, the most effective current solution is the CPU-side NumPy + Numba combination (with thread tuning). The GPU path still has room for improvement through better kernel fusion and less small-kernel scheduling overhead.

## 7. Note

To keep the report reproducible, this document references only existing CSV outputs and does not include new reruns in this round.
