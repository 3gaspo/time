# Foundation-model results

## Current foundation benchmark

The current synchronized run completed the deterministic Seasonal-Naive and
finite-pair scaled-MASE contract. Each of the four models has 98 completed and
timed dataset/frequency/term tasks across 50 dataset/frequency cells. The
dependent summary and feature analysis also completed.

| Model | Target modes | Scaled MASE | Inference seconds |
|---|---|---:|---:|
| Chronos-2 | multivariate, univariate | 0.685489 | 433.767 |
| TS-ICL | univariate | 0.718394 | 2777.139 |
| Chronos-Bolt | univariate | 0.759559 | 957.030 |
| Seasonal Naive | univariate | 1.000000 | 654.467 |

Lower scaled MASE is better. Chronos-2 is the strongest learned model under
this benchmark, reducing scaled MASE by 4.58% relative to TS-ICL and by 9.75%
relative to Chronos-Bolt. It is also the fastest learned-model evaluation in
the synchronized timing totals. Seasonal Naive is the deterministic taskwise
normalizer, so its scaled score is exactly one.

## Chronos-2 channel comparison

The current channel run completed all 74 task manifests for each of the 38
multivariate dataset/frequency cells:

| Representation | Scaled MASE | Inference seconds | Terminal workflow state |
|---|---:|---:|---|
| Native multivariate | 0.690045 | 335.599 | summary failed |
| Independent univariate | 0.695590 | 349.749 | summary failed |
| Past targets as covariates | 0.690045 | 1924.845 | completed |

Native multivariate and past-target-covariate forecasting each improve the
geometric-mean score by 0.80% relative to independent univariate forecasting.
They are numerically indistinguishable at the task level for this evidence:
their scaled-MASE difference is below `1e-6` on all 74 tasks and below
`3.8e-7` at its maximum. The covariate route nevertheless takes 5.74 times the
native-multivariate inference time. The evidence therefore supports a small
benefit from cross-channel information, but not the additional cost of
expressing that information through separate past-target covariates when
native multivariate Chronos-2 is available.

The native-multivariate and independent-univariate jobs are classified as
evaluation-complete but workflow-incomplete. Both reached their summary stage
before the matching Seasonal Naive job finished. Native multivariate stopped
on a missing positive baseline for `Crypto/D/short`, and independent
univariate stopped on `MetroPT-3/5T/long`. Their figures above were reconstructed
directly from all 74 completed task metrics and the subsequently completed
matching Seasonal Naive metrics. Canonical summary artifacts still need to be
regenerated; no channel inference rerun is required.

## Feature associations

The completed feature analysis selected temporal heterogeneity (mean absolute
Spearman correlation 0.467), trend Hurst exponent (0.411), temporal scale
heterogeneity (0.398), temporal location heterogeneity (0.392), and the second
period (0.376) as the five strongest associations with model scaled MASE.
Seasonal Naive is constant at one, so its within-model feature correlations are
correctly undefined and excluded from these ranking means. These associations
are descriptive across the 50 dataset/frequency cells, not causal evidence.

## Evidence boundary

The synchronized lightweight publication contains completed manifests,
configuration, compact task metrics, workflow records, aggregate tables, and
logs, but omits the heavy prediction and per-window metric arrays. The
conclusions above are therefore verified at the task/report contract level;
per-window reanalysis would require a detailed artifact synchronization.
