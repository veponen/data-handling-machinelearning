# Data Tour

The earlier example files showed only one or two records. This tour introduces
the full artificial Edge-LMS dataset and helps you learn how its files and
tables fit together before project analysis begins.

Some public datasets, including many Kaggle datasets, are already arranged as
one analysis-ready table. Application data often begin as several related
records with different identifiers, timestamps, row meanings, and missing-value
mechanisms. We start with the normalized `student-analysis` release so that you
can learn these relationships before later source-like ETL work.

## Start

1. Download and extract [edge-lms-data-tour.zip](data/edge-lms-data-tour.zip).
2. Open the extracted `README.md`.
3. Open `notebooks/00-dataset-tour.ipynb` in Jupyter or VS Code.

Keep the supplied `data/student-analysis/` folder unchanged. Save your own
notebook, notes, and figures elsewhere.

Edge-LMS activity is observable only on Mondays. Tuesday–Sunday records mean
that LMS study was structurally unobserved—not that the student was inactive.

All data are artificial. Never add your own or a classmate's real data. This is
a familiarization activity, not a completed analysis or modelling task.
