# 🎬 Movie Lens Dataset — README

## Overview

This dataset is a merged version of the **MovieLens** dataset originally published by GroupLens Research and sourced from Kaggle. It combines movie ratings, tags, and metadata into a single flat file, making it ready for exploratory analysis, recommendation systems, and NLP/ML experiments.

---

## Dataset Summary

| Property | Value |
|---|---|
| **Total Records** | 100,836 rows |
| **Total Columns** | 7 |
| **Unique Movies** | 9,742 |
| **Unique Users** | 610 |
| **Rating Range** | 0.5 — 5.0 |
| **Date Range** | March 1996 — September 2018 |
| **File Format** | CSV (comma-separated) |
| **Source** | Kaggle / GroupLens MovieLens |

---

## File Structure

```
movie_data.csv
```

---

## Columns

| Column | Type | Description |
|---|---|---|
| `movieId` | Integer | Unique identifier for each movie |
| `userId` | Integer | Unique identifier for each user |
| `genres` | String | Pipe-separated list of genres (e.g. `Action\|Comedy\|Drama`) |
| `title` | String | Movie title including release year in parentheses (e.g. `Toy Story (1995)`) |
| `tag` | String | Free-text tag applied by the user to the movie |
| `timestamp` | Integer | Unix timestamp of the rating or tag event |
| `rating` | Float | User rating on a scale of 0.5 to 5.0 (in 0.5 increments) |

---

## Missing Values

| Column | Missing Rows | Notes |
|---|---|---|
| `movieId` | 91,094 | Rows without movie metadata (rating-only rows) |
| `genres` | 91,094 | Only populated when movie metadata is present |
| `title` | 91,094 | Only populated when movie metadata is present |
| `tag` | 97,153 | Tags are sparse — most rows are ratings without tags |
| `userId` | 0 | Always present |
| `timestamp` | 0 | Always present |
| `rating` | 0 | Always present |

---

## Rating Distribution

| Rating | Count |
|---|---|
| 0.5 | 1,370 |
| 1.0 | 2,811 |
| 1.5 | 1,791 |
| 2.0 | 7,551 |
| 2.5 | 5,550 |
| 3.0 | 20,047 |
| 3.5 | 13,136 |
| 4.0 | 26,818 ⭐ most common |
| 4.5 | 8,551 |
| 5.0 | 13,211 |

Average rating: **3.50**

---

## Top Genres

| Genre | Movie Count |
|---|---|
| Drama | 4,361 |
| Comedy | 3,756 |
| Thriller | 1,894 |
| Action | 1,828 |
| Romance | 1,596 |
| Adventure | 1,263 |
| Crime | 1,199 |
| Sci-Fi | 980 |
| Horror | 978 |
| Fantasy | 779 |

---

## Potential Use Cases

- **Collaborative Filtering** — build a user-based or item-based recommendation system
- **Content-Based Filtering** — use genres and tags to recommend similar movies
- **NLP on Tags** — analyze free-text tags for sentiment or topic modeling
- **Rating Prediction** — regression or classification task to predict user ratings
- **EDA / Visualization** — explore trends in genres, ratings over time, user behavior

---

## How to Load

```python
import pandas as pd

df = pd.read_csv('movie_data.csv')
print(df.shape)       # (100836, 7)
print(df.head())
print(df.dtypes)
```

---

## Notes

- The `timestamp` column is in **Unix epoch format**. Convert it using:
  ```python
  import pandas as pd
  df['date'] = pd.to_datetime(df['timestamp'], unit='s')
  ```
- The `genres` column contains **pipe-separated values**. Split them with:
  ```python
  df['genres'].str.split('|')
  ```
- Movie release year is **embedded in the title** column and can be extracted with:
  ```python
  df['year'] = df['title'].str.extract(r'\((\d{4})\)')
  ```

---

## License

This dataset originates from the [MovieLens project](https://grouplens.org/datasets/movielens/) by GroupLens Research at the University of Minnesota. Please refer to their terms of use for redistribution and usage rights.
