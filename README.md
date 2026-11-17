# Office Occupancy Detector

Detect room occupancy from environmental sensor readings using a forward-in-time holdout.

## Dataset

[UCI Occupancy Detection dataset](https://archive.ics.uci.edu/dataset/357/occupancy%2Bdetection) (dataset ID 357), 20,560 records. The source is public and is fetched by the runner; the raw dataset is not committed.

## Run

```bash
python -m pip install -r requirements.txt
python main.py --output-dir artifacts
```

The runner saves metrics, holdout predictions, and a reusable model in the ignored output directory. The public [`reports/benchmark.json`](reports/benchmark.json) contains aggregate results only; no row-level records are published.

## Holdout results

The records are sorted by the dataset timestamp and split forward in time (70% train, 30% holdout).

| Accuracy | Balanced accuracy | Macro F1 | Weighted F1 | Majority baseline accuracy |
|---:|---:|---:|---:|---:|
| 0.898 | 0.936 | 0.855 | 0.906 | 0.822 |

ROC-AUC: **0.981**.

Full aggregate metrics and the exact split seed are in [`reports/benchmark.json`](reports/benchmark.json).

## Limits

The forward split is based on the dataset's row timestamp order, but is a single-site benchmark. Evaluate on other buildings, seasons, and sensor installations before operational use. These are one-time benchmark results, not service-level, production, or causal claims.

## Reproducibility

The model and split use seed 42. Re-running downloads source data from UCI and regenerates local artifacts. Model binaries, raw inputs, and row-level predictions are excluded from this public repository.
