# Data Analyst Portfolio

A personal portfolio website built with Django, featuring an interactive machine learning demo that classifies iris flowers.

## Features

- **Portfolio site** with tabs for home, projects, CV and contact (bio, CV and contact content is still placeholder text).
- **Iris classifier** (`/iris/`): enter sepal and petal measurements and get the predicted species (Setosa, Versicolor or Virginica) with its image.
- **Project cards** for house price and diabetes models, planned but not implemented yet.

## Tech stack

- Python and Django
- scikit-learn, pandas and NumPy
- Bootstrap 5 and SweetAlert2 for the front end

## Getting started

Requires Python 3.11 or later.

```bash
git clone https://github.com/angelherrerog/data_analyst_web.git
cd data_analyst_web

python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

cd proyect
python manage.py runserver
```

Then open `http://127.0.0.1:8000/` for the portfolio and `http://127.0.0.1:8000/iris/` for the classifier. Stop the server with `Ctrl + C`.

## The Iris model

The classifier is an SVC with feature scaling, trained on the iris dataset bundled with scikit-learn and saved as `temp/classification_svc_latest.pickle`.

Pickle files depend on the scikit-learn version that created them. If loading fails with a different version installed, retrain and save the model again:

```python
import pickle
from sklearn.datasets import load_iris
from sklearn.pipeline import make_pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.svm import SVC

iris = load_iris()
model = make_pipeline(StandardScaler(), SVC()).fit(iris.data, iris.target)

with open("temp/classification_svc_latest.pickle", "wb") as f:
    pickle.dump(model, f)
```

## Project structure

```text
proyect/
  manage.py
  proyect/            Django project settings and root URLs
  portfolio_app/      Views, URLs and templates (index, iris)
  static/             CSS, JavaScript and images
temp/                 Trained models and original course assets
docs/GUIA_CURSO.md    Step-by-step course guide (in Spanish)
requirements.txt
```

## Credits

Based on the Udemy course "Python para el análisis de datos" by Erick Hernández, adapted from [lucrae/django-cheat-sheet](https://github.com/lucrae/django-cheat-sheet/). The original step-by-step guide is kept in [docs/GUIA_CURSO.md](docs/GUIA_CURSO.md).
