# 03 · ML Fundamentals

Classical ML done right: from raw data to a deployed model.

## Algorithms to master

| Algorithm | When to use it |
|---|---|
| Linear / Logistic Regression | Always your baseline. If it works, don't overcomplicate. |
| Random Forest | Tabular data, robust, few surprises |
| XGBoost / LightGBM | Kaggle competitions and real production |
| K-means | Exploration and segmentation without labels |
| SVM | Small datasets and high dimensionality |

## Notebooks

| Notebook | Topic |
|---|---|
| `01_regression.ipynb` | Linear regression from scratch and with sklearn |
| `02_classification.ipynb` | Random Forest + full evaluation |
| `03_clustering.ipynb` | K-means on real data |
| `04_feature_engineering.ipynb` | Turning raw data into useful features |
| `05_evaluation.ipynb` | Metrics, cross-validation, overfitting |

## Project: sentiment classifier

Folder: [`project/`](./project/)

```
project/
├── data/           ← dataset (don't commit to git)
├── notebooks/      ← exploration and experimentation
├── src/
│   ├── preprocess.py
│   ├── train.py
│   └── predict.py
├── app.py          ← Streamlit interface
├── requirements.txt
└── README.md
```

### How to run

```bash
cd project
pip install -r requirements.txt
python src/train.py
streamlit run app.py
```

## Resources

- [Andrew Ng - ML Specialization](https://www.coursera.org/specializations/machine-learning-introduction)
- [Scikit-learn User Guide](https://scikit-learn.org/stable/user_guide.html)
- [Kaggle Learn - Intermediate ML](https://www.kaggle.com/learn/intermediate-machine-learning)
