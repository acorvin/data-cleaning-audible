# Data Cleaning: Audible Dataset

The purpose of this project is to prepare a dataset for further analysis, visualization, or machine learning tasks. This project is aimed at cleaning and preprocessing a dataset related to Audible, a popular audiobook and spoken-word entertainment platform. The dataset contains information about audiobooks, such as titles, authors, durations, and ratings.

### Dataset

`audible_uncleaned.csv` (included) has 87,489 audiobook listings in 36 languages, with these columns:

| Column | Raw format |
|---|---|
| `name` | Title |
| `author` | `Writtenby:RickRiordan` |
| `narrator` | `Narratedby:RobbieDaymond` |
| `time` | `13 hrs and 8 mins` |
| `releasedate` | `01-05-18` (day-month-year) |
| `language` | `English` |
| `stars` | `4.5 out of 5 stars41 ratings` or `Not rated yet` |
| `price` | `820.00` |

### Cleaning steps

All of the work is in [`audible_cleaning.ipynb`](audible_cleaning.ipynb):

1. **Remove duplicate rows.**
2. **Clean author and narrator names.** Strip the `Writtenby:` and `Narratedby:` prefixes, then add a space between joined first and last names (`RickRiordan` becomes `Rick Riordan`).
3. **Extract the star rating.** Pull the number out of the `stars` text into a new numeric `star_rating` column (`4.5 out of 5 stars41 ratings` becomes `4.5`).
4. **Drop unrated titles.** Remove listings marked `Not rated yet`.
5. **Drop unused columns.** Remove the original `stars` text and `price`.
6. **Standardize release dates.** Convert `01-05-18` to ISO format, `2018-05-01`.
7. **Standardize running time.** Convert `13 hrs and 8 mins` to `13:08:00`, stored in a new `duration` column.

### Result

The cleaned table has 15,072 rated audiobooks and 7 columns: `name`, `author`, `narrator`, `releasedate`, `language`, `star_rating`, and `duration`. Most of the drop from 87,489 rows comes from removing unrated titles.

### How to run

```bash
pip install pandas numpy jupyter
jupyter notebook audible_cleaning.ipynb
```

The notebook reads `audible_uncleaned.csv` from the same folder and keeps the cleaned table in memory as `df`. Add `df.to_csv("audible_cleaned.csv", index=False)` at the end to save it.

### Technologies

**[Python](https://www.python.org/)**

**[pandas](https://pandas.pydata.org/)**

**[NumPy](https://numpy.org/)**
