# Taller2-P2-AnalisisDatos

Data analysis of IMDB movie metadata, built as an assignment workshop. The repository contains a Google Colab notebook that answers eight analytics questions about movies (score distributions, counts by color, yearly production, and a world map of average scores), plus a small Django application that renders a choropleth map of movie counts per country.

## Features

Notebook (`123456789.ipynb`):

- Downloads the movie dataset and the Natural Earth country shapefile at runtime.
- Histograms of `imdb_score` for French and Canadian films, and for black-and-white films.
- Bar chart of the average `imdb_score` per country.
- Count of black-and-white versus color films.
- Bar chart of Christopher Nolan films by `imdb_score`.
- Line chart of USA film production from 2010 to 2015.
- World choropleth map of the average `imdb_score` per country (geopandas and matplotlib).

Django application (`IMDBAnalyticsProject/`):

- `Movie` and `Map` models; the `Map` model stores the uploaded shapefile components.
- A `home` view that counts movies per country, merges them with the country geometries, and renders a Plotly choropleth map (`analytics/templates/home.html`).
- Django admin for the `Movie` and `Map` models.

## Tech stack

- Python
- Jupyter / Google Colab notebook
- pandas, NumPy, matplotlib, Plotly, GeoPandas
- Django 4.1 (migrations were generated with Django 4.1.7), SQLite
- Natural Earth 10m admin-0 countries shapefile

## Project structure

```
.
├── 123456789.ipynb            # Colab notebook with the workshop answers
├── MapaCreado.pdf             # Screenshot of the generated world map
└── IMDBAnalyticsProject/
    ├── manage.py
    ├── IMDBAnalytics/         # Django project settings and root URL configuration
    ├── analytics/             # Django app: models, migrations, home view, template
    ├── db.sqlite3             # SQLite database used by the Django app
    └── media/                 # Natural Earth country shapefile (ne_10m_admin_0_countries)
```

## Getting started

### Notebook (Google Colab)

1. Open `123456789.ipynb` in Google Colab.
2. Run the cells in order. The first cells download and unzip the data into `/content/IMDBAnalyticsData/`, and the `pip install geopandas` cell installs the geospatial dependency.

The notebook expects `IMDBAnalyticsData/Data/movie_metadata.csv` and the shapefile under `IMDBAnalyticsData/Data/Map/`. These files are not stored in this repository.

To run the notebook locally, install the imports it uses (no requirements file is provided):

```bash
pip install pandas numpy matplotlib plotly geopandas jupyter
jupyter notebook 123456789.ipynb
```

The notebook also expects the data files at the paths above, so the first download cell must be adapted or the files placed manually.

### Django application

```bash
cd IMDBAnalyticsProject
pip install django pandas geopandas plotly
python manage.py runserver
```

Then open http://127.0.0.1:8000/ in a browser. The `home` view expects at least one `Map` row (pointing to an uploaded shapefile) and `Movie` rows in `db.sqlite3`. This repository does not document how to load them, and the contents of the committed database were not checked.

Admin is available at http://127.0.0.1:8000/admin/.

## Context

This is coursework: the notebook is a workshop template (Spanish-language questions, with a placeholder for the student's name) and the Django project is a companion application for the same dataset. The repository name indicates a second-part assignment (Taller 2, P2).

## Notes

- The Django settings are for development only: `DEBUG = True`, an empty `ALLOWED_HOSTS`, and a hard-coded `SECRET_KEY` in `IMDBAnalytics/settings.py`.
- The data files are downloaded at runtime and are not included in the repository.
