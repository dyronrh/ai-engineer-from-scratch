# Project · Sentiment Classifier

First complete project: a text classifier deployed as a web app.

## What it does

Takes a piece of text and returns whether the sentiment is positive, negative or neutral, along with a confidence score.

## Stack

- **ML:** scikit-learn (TF-IDF + Logistic Regression / Random Forest)
- **Web app:** Streamlit
- **Dataset:** IMDb 50K reviews

## Getting started

```bash
cd phase-1-foundations/03-ml-fundamentals/project
pip install -r requirements.txt

# download the dataset (instructions in data/README.md)

python src/train.py
streamlit run app.py
```

## Structure

```
project/
├── data/
│   └── README.md           ← instructions for downloading the dataset
├── notebooks/
│   └── 01_exploration.ipynb
├── src/
│   ├── preprocess.py       ← cleaning and tokenization
│   ├── train.py            ← training and model saving
│   └── predict.py          ← inference function
├── app.py                  ← Streamlit interface
├── requirements.txt
└── README.md
```

## What it demonstrates

- Complete end-to-end pipeline
- Honest evaluation (correct train/val/test split)
- Functional app someone can actually use
- Code organized into modules

## Success criteria

- Accuracy > 85% on the test set
- App runs without errors
- Code has type hints
- README explains how to reproduce results
