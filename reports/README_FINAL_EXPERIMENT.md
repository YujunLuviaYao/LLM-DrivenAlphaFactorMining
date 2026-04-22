# LLM Alpha Mining Final Acceleration Report (Latest)

- Methods: Baseline, Opt1, Opt2, Opt3, Opt4, Opt5, Opt6, Opt6 Full

## 1. Source Files

- `results/timing/baseline_timing.csv`
- `results/timing/opt1_timing.csv`
- `results/timing/opt2_timing.csv`
- `results/timing/opt3_timing.csv`
- `results/timing/opt4_timing.csv`
- `results/timing/opt5_timing.csv`
- `results/timing/opt6_timing.csv`
- `results/timing/opt6_full_timing.csv`
- `results/timing/final_submission_summary.csv`

## 2. Final Results (Same format as final tables)

### Table 4: Factor computation runtime

| Method | Comp. (s) | Speedup |
|---|---:|---:|
| Baseline | 1819.37 | 1.00x |
| Opt1 | 1814.62 | 1.00x |
| Opt2 | 10.37 | 175.4x |
| Opt3 | 3.66 | 497.5x |
| Opt4 | 3.37 | 539.4x |
| Opt5 | 3.21 | 567.0x |
| Opt6 | 0.87 | 2099.2x |
| Opt6 Full | 0.68 | 2680.2x |

### Table 5: Factor evaluation runtime

| Method | Eval. (s) | Speedup |
|---|---:|---:|
| Baseline | 191.40 | 1.00x |
| Opt1 | 158.36 | 1.21x |
| Opt2 | 197.35 | 0.97x |
| Opt3 | 190.80 | 1.00x |
| Opt4 | 195.51 | 0.98x |
| Opt5 | 188.24 | 1.02x |
| Opt6 | 162.34 | 1.18x |
| Opt6 Full | 35.82 | 5.34x |

## 3. Note

- The two speedup columns above are computed separately:
  - Table 4 speedup = `baseline compute / method compute`
  - Table 5 speedup = `baseline evaluate / method evaluate`
- `final_submission_summary.csv` also keeps total runtime (`compute + evaluate`) for reference.
