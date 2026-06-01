# Phase 1 · Foundations

> The base everything else sits on. No shortcuts here.

**Estimated duration:** 4–8 weeks  
**Commitment:** 10–15 hours per week

---

## What you'll be able to do after this phase

- Write async, typed, object-oriented Python for real AI projects
- Understand the math behind ML algorithms (not memorize - understand)
- Train, evaluate and select classical machine learning models
- Complete the phase project: a deployed sentiment classifier

---

## Modules

### [01 · Python for AI](./01-python-for-ai/)

The Python used in real AI projects is not beginner Python. You need async/await for API calls, type hints to keep code readable as projects grow, and NumPy + Pandas to work with data.

**Topics:**
- `async/await` and asynchronous programming
- OOP: classes, inheritance, protocols
- Type hints and mypy
- NumPy: arrays, broadcasting, vectorized operations
- Pandas: DataFrames, groupby, merge, data cleaning
- Matplotlib and Seaborn: exploratory visualization

**Resources:**
| Resource | Time |
|---|---|
| [Real Python - Async IO](https://realpython.com/async-io-python/) | 1 week |
| [Python Docs - typing](https://docs.python.org/3/library/typing.html) | 3 days |
| [Kaggle Learn - Python + Pandas](https://www.kaggle.com/learn) | 1 week |

---

### [02 · Math & Statistics](./02-math-and-stats/)

You don't need to be a mathematician, but you do need to understand what the code is doing underneath. Without this, debugging a broken model means guessing.

**Topics:**
- Linear algebra: vectors, matrices, matrix multiplication, eigenvalues
- Calculus: derivatives, chain rule (that's basically backprop), gradients
- Probability: distributions, Bayes theorem, expected value
- Statistics: mean, variance, correlation, basic hypothesis testing

**Resources:**
| Resource | Time |
|---|---|
| [3Blue1Brown - Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) | 1 week |
| [3Blue1Brown - Calculus](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) | 1 week |
| [StatQuest - Probability & Statistics](https://www.youtube.com/@statquest) | 2 weeks |

---

### [03 · ML Fundamentals](./03-ml-fundamentals/)

Classical machine learning: regression, classification, clustering. Scikit-learn is your main tool here. Beyond training models, you'll learn to evaluate them properly - which is more than half the real work.

**Topics:**
- Linear and logistic regression
- Decision trees, Random Forest, XGBoost
- Clustering: K-means, DBSCAN
- Evaluation metrics: accuracy, precision, recall, F1, AUC-ROC
- Overfitting, regularization, cross-validation
- Feature engineering and feature selection

**Resources:**
| Resource | Time |
|---|---|
| [Andrew Ng - ML Specialization](https://www.coursera.org/specializations/machine-learning-introduction) | 4 weeks |
| [Scikit-learn - Official tutorial](https://scikit-learn.org/stable/tutorial/index.html) | 1 week |
| [Kaggle - Feature Engineering](https://www.kaggle.com/learn/feature-engineering) | 3 days |

---

## Phase project

**Deployed sentiment classifier**

Build a model that classifies text as positive, negative or neutral, and expose it as a simple web app.

**Stack:** Python · Scikit-learn · Streamlit  
**Dataset:** [IMDb reviews](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews) or [Twitter Sentiment](https://www.kaggle.com/datasets/kazanova/sentiment140)

**What you'll demonstrate:**
- Full pipeline: raw data → features → model → evaluation
- Functional web interface with Streamlit
- Clean, typed code

Project folder: [`03-ml-fundamentals/project/`](./03-ml-fundamentals/project/)

---

## Phase checklist

- [ ] Wrote at least one Python script using `async/await`
- [ ] Implemented a class with type hints
- [ ] Manipulated a dataset with Pandas (groupby, merge, cleaning)
- [ ] Can explain what a gradient is without looking it up
- [ ] Trained at least 3 different ML algorithms
- [ ] Evaluated a model using more than one metric
- [ ] Sentiment classifier runs on Streamlit

When you're done, move on to [Phase 2 · AI Core](../phase-2-ai-core/).
