# Learning Polars
Repo to keep some code snippets with polars or its equivalents with pandas (or spark or dplyr)

Polars is very fast. In fact, it is one of the best performing solutions available. See the results in [DuckDB's db-benchmark](https://duckdblabs.github.io/db-benchmark/).

More on polars on its [github](https://github.com/pola-rs/polars).

## Links and sources for polars code snippets
 - Complex groupby clauses in polars: [stackoverflow](https://stackoverflow.com/questions/75498169/ambiguous-results-when-apply-filter-in-polars-groupby-context)
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


