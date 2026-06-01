# 01 · MLOps

Infrastructure that keeps AI projects alive and reproducible.

## Why this matters

Without MLOps:
- You can't reproduce last month's results
- You don't know which model is running in production
- Deploying a new model takes a whole day
- A bad dataset update breaks everything silently

## Experiment tracking with MLflow

Every training run logs:
- Parameters (learning rate, model name, chunk size...)
- Metrics (accuracy, loss, F1, latency...)
- Artifacts (model file, confusion matrix, sample outputs)

```python
import mlflow

with mlflow.start_run():
    mlflow.log_param("model", "gpt-4o")
    mlflow.log_param("chunk_size", 512)
    mlflow.log_metric("faithfulness", 0.87)
    mlflow.log_metric("relevance", 0.91)
```

## Data versioning with DVC

```bash
dvc init
dvc add data/raw/dataset.csv
git add data/raw/dataset.csv.dvc .gitignore
git commit -m "track dataset with DVC"
```

## CI/CD with GitHub Actions

Automate: test → lint → train → evaluate → deploy.

```yaml
# .github/workflows/ml_pipeline.yml
on: [push]
jobs:
  test-and-eval:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: pip install -r requirements.txt
      - run: pytest tests/
      - run: python evaluate.py --threshold 0.85
```

## Exercises

| Exercise | File | Description |
|---|---|---|
| 1 | `01_mlflow_tracking.py` | Log a full experiment with MLflow |
| 2 | `02_dvc_pipeline.py` | DVC pipeline for a ML workflow |
| 3 | `03_github_actions/` | CI/CD workflow for a model |

## Resources

- [MLflow Docs](https://mlflow.org/docs/latest/index.html)
- [DVC Docs](https://dvc.org/doc)
- [GitHub Actions for ML](https://docs.github.com/en/actions)
