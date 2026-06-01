# Phase 1 - Foundations

**Estimated duration:** 4-6 weeks  
**Commitment:** 10-15 hours per week

---

## Reality check before you start

Based on analysis of thousands of AI Engineer job postings, here is what Phase 1 actually means for your career:

**Python skills:** appear in 82% of all AI Engineer postings. This is the most important thing you can do in Phase 1.

**Math skills:** appear explicitly in fewer than 20% of postings, and mostly for ML Engineer roles (training models from scratch). If your goal is AI Engineer or LLM Engineer, spend less time here and come back later if needed.

**ML fundamentals:** useful for context and understanding, not a hard requirement for most production AI Engineer roles.

---

## Modules

### [01 - Python for AI](./01-python-for-ai/) — do this first, take your time

The Python that production AI projects use. Not beginner Python - async, typed, and tool-friendly.

**Topics:**
- `async/await` - you will use this for every API call
- OOP and type hints - code that doesn't fall apart at 1000 lines
- NumPy: arrays, broadcasting, vectorized operations
- Pandas: DataFrames, groupby, merge, cleaning
- Matplotlib/Seaborn: quick visualizations

**Resources:**
| Resource | Time |
|---|---|
| [Real Python - Async IO](https://realpython.com/async-io-python/) | 1 week |
| [Python Docs - typing](https://docs.python.org/3/library/typing.html) | 3 days |
| [Kaggle Learn - Python + Pandas](https://www.kaggle.com/learn) | 1 week |

---

### [02 - Math and Statistics](./02-math-and-stats/) — useful, not blocking

Good to have, not a hard requirement for most AI Engineer roles. If you're in a hurry, do 1 week of linear algebra and move on. Come back for the rest later.

If you want ML Engineer roles (training your own models), invest the full time here.

**Topics:**
- Linear algebra: vectors, matrices, dot product, eigenvalues
- Calculus: derivatives and chain rule (this is what backprop is)
- Probability and statistics: distributions, Bayes, mean and variance

**Resources:**
| Resource | Time |
|---|---|
| [3Blue1Brown - Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) | 1 week |
| [3Blue1Brown - Calculus](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) | 1 week |
| [StatQuest - Probability and Statistics](https://www.youtube.com/@statquest) | 1 week |

---

### [03 - ML Fundamentals](./03-ml-fundamentals/) — for context

Classical machine learning. Scikit-learn is your tool here. The goal is not to become a data scientist - it's to understand what models do so you can use them intelligently.

**Topics:**
- Linear and logistic regression
- Random Forest and XGBoost
- Evaluation: accuracy, precision, recall, F1, AUC
- Overfitting, cross-validation, feature engineering

**Resources:**
| Resource | Time |
|---|---|
| [Andrew Ng - ML Specialization](https://www.coursera.org/specializations/machine-learning-introduction) | 3 weeks |
| [Scikit-learn - Official tutorial](https://scikit-learn.org/stable/tutorial/index.html) | 1 week |
| [Kaggle - Feature Engineering](https://www.kaggle.com/learn/feature-engineering) | 3 days |

---

## Phase project

**Deployed sentiment classifier**

Text classifier with a Streamlit frontend. The point is to complete the full cycle: data, model, evaluation, deployment. Not to get a perfect accuracy.

**Stack:** Python, Scikit-learn, Streamlit  
**Dataset:** [IMDb 50K reviews](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews)

Project folder: [`03-ml-fundamentals/project/`](./03-ml-fundamentals/project/)

---

## Phase checklist

- [ ] Can write async Python and explain why it matters for API calls
- [ ] Built a typed class with type hints
- [ ] Cleaned a real dataset with Pandas
- [ ] Can explain gradient descent without looking it up
- [ ] Trained 3 different classifiers and compared them
- [ ] Sentiment classifier runs on Streamlit

Next: [Phase 2 - AI Core](../phase-2-ai-core/)
