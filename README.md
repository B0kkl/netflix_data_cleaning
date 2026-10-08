# Netflix Data Cleaning

**Project URL:** https://github.com/B0kkl/netflix_data_cleaning

Cleaning the [Netflix Movies and TV Shows dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows) from Kaggle using **Python, Pandas and Jupyter Notebook**.

The goal is not just to drop nulls, but to understand why values are missing and make a deliberate decision for each column.

## What the raw data looked like

- 8,807 rows, 12 columns, no duplicate rows or duplicate `show_id` values.
- Missing values: `director` 2,634 (29.9%), `country` 831 (9.4%), `cast` 825 (9.4%), `date_added` 10, `rating` 4, `duration` 3.
- `date_added` was stored as text, and 88 values had a leading space.
- `duration` mixed minutes ("90 min") for movies with seasons ("2 Seasons") for TV shows.
- Three titles had their runtime ("74 min", "84 min", "66 min") typed into the `rating` column, with `duration` left empty.

## Cleaning decisions

| Column | Decision | Reason |
|---|---|---|
| `director`, `cast`, `country` | Filled with "Unknown" | Many titles legitimately have no listed value. Dropping them would delete thousands of valid titles. |
| `rating` / `duration` | Moved the 3 misplaced runtimes into `duration`, then filled remaining missing ratings with "Not Rated" | The values were in the wrong column, not missing. |
| `date_added` | Stripped spaces and converted to `datetime` | Text dates cannot be sorted or filtered by month/year. |
| `duration` | Split into `duration_value` (number) and `duration_unit` | A number can be averaged; the unit keeps minutes and seasons separate. |

The 10 missing `date_added` values were left as missing, because inventing a date would be misleading.

## How to run

```bash
git clone https://github.com/B0kkl/netflix_data_cleaning.git
cd netflix_data_cleaning
pip install pandas jupyter
jupyter notebook
```

Open the notebook and run the cells from top to bottom. The raw file must be in the folder the notebook expects.

## Project structure

```
netflix_data_cleaning/
├── raw_data/            raw Kaggle CSV
├── <your-notebook>.ipynb
├── <cleaned-file>.csv   cleaned output
└── README.md
```

Edit the file names above so they match the files in your repo.
