# Foundation-model benchmark summary

Each task MASE is divided by the matching Seasonal Naive MASE, then task ratios are combined with the TIME leaderboard geometric mean. Inference seconds are summed over the same test forecasting tasks; a blank total means at least one task lacks timing metadata.

| Model | Target mode | State | Exit | Scaled MASE (GM) | Inference seconds | Datasets | Tasks | Timed tasks |
|---|---|---|---:|---:|---:|---:|---:|---:|
| chronos2 | multivariate,univariate | completed | 0 | 0.685489 | 430.503 | 50 | 98 | 98 |
| ts_icl | univariate | completed | 0 | 0.718394 | 2759.578 | 50 | 98 | 98 |
| chronos_bolt | univariate | completed | 0 | 0.759559 | 956.998 | 50 | 98 | 98 |
| seasonal_naive | univariate | completed | 0 | 1.000000 | 650.595 | 50 | 98 | 98 |
| timesfm3 |  | failed | 1 |  |  | 0 | 0 | 0 |
