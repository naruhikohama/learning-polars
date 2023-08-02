# Learning Polars
Repo to keep some code snippets with polars or its equivalents with pandas (or spark or dplyr)

Polars is very fast. In fact, it is one of the best performing solutions available. See the results in [DuckDB's db-benchmark](https://duckdblabs.github.io/db-benchmark/).

Polars cheatsheet: https://franzdiebold.github.io/polars-cheat-sheet/Polars_cheat_sheet.pdf

More on polars on its [github](https://github.com/pola-rs/polars) and on this [repo](https://github.com/ddotta/awesome-polars), also on github.

## Links and sources for polars code snippets
 - Groupby with filter in polars: [stackoverflow](https://stackoverflow.com/questions/75498169/ambiguous-results-when-apply-filter-in-polars-groupby-context)
```python
import polars as pl

df = pl.DataFrame(
    {
        "day": [2, 2, 2, 2, 2, 2, 1, 1],
        "y": [4, 5, 8, 7, 9, None, None, None],
        "x": [1, 2, 3, 4, 5, 6, 1, 2],
    }
)

xcol = "x"
ycol = "y"
f = pl.all(pl.col(["x", "y"]).is_not_null())

df.groupby("day").agg(
    (pl.col(xcol) - pl.col(xcol).filter(f).mean()).filter(f).sum().alias("filered_sum")
)
```
 - Groupby with lambda function
```python
df.groupby(by="groups").agg(
     [
          # Count the number of values in each group
          pl.count("random").alias("size"),

          # Sample one element in each group
          pl.col("names").apply(
               lambda group_df: group_df.sample(1)
          ),
     ]
)
```

