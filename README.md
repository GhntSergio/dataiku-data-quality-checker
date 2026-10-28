# Dataiku Data Quality Checker

Automated data quality profiling for tabular datasets, usable as a **standalone CLI** or inside a **Dataiku DSS Python recipe**. It produces an HTML report plus distribution charts in one run.

## What it checks

| Check | Output |
|---|---|
| Missing values | Count and % per column, sorted |
| Duplicates | Number of duplicated rows |
| Data types | Detected type per column |
| Cardinality | Unique values per column |
| Descriptive statistics | Mean, std, min/max, quartiles |
| Outliers | Outlier detection on numeric columns |
| Distributions | One histogram per numeric column (PNG) |

Supported formats: **CSV, Excel (.xlsx/.xls), Parquet**.

## Usage

### Command line

```bash
pip install pandas numpy seaborn matplotlib openpyxl pyarrow
python data_quality_checker.py path/to/dataset.csv
```

The report and charts are written to `data_quality_reports/`.

### Inside a Dataiku DSS Python recipe

```python
import dataiku
from data_quality_checker import run_quality_check

df = dataiku.Dataset("my_dataset").get_dataframe()
results = run_quality_check(df, output_name="my_dataset")

results["missing"]   # DataFrame of missing values
results["outliers"]  # DataFrame of detected outliers
```

`run_quality_check` returns a dictionary of DataFrames (`missing`, `duplicates`, `types`, `cardinality`, `stats`, `outliers`) so results can be pushed to output datasets or used in scenario checks.

## Tech stack

Python · pandas · NumPy · seaborn · Matplotlib · Dataiku DSS

## License

MIT
