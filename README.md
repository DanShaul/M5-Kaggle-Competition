# M5 Kaggle Competition Forecasting

This project explores demand forecasting for the Walmart M5 Kaggle dataset.

The main work is in the `code/` folder:

- `code/light_gbm.ipynb` trains and evaluates a LightGBM forecasting model.
- `code/creating-snaive-baseline.ipynb` creates a seasonal naive baseline.
- `code/info.md` contains project notes.

## Project Structure

```text
code/          Notebooks and project notes
data/          Kaggle M5 ZIP file and small supporting data
models/        Saved trained model artifacts
pickles/       Prepared train/test datasets used by notebooks
predictions/   Saved validation and baseline predictions
```

## Current Modeling Setup

The LightGBM workflow uses a CV split where the last 28 days are validation data.
Forecasting is done recursively, one day at a time, so lag and rolling features for future days use previous predictions instead of future actual sales.

The validation prediction output is saved to:

```text
predictions/lightgbm_validation_predictions.csv
```

## Metrics

The notebooks report standard item-day metrics:

- MAE
- RMSE
- WAPE

The LightGBM notebook also calculates WRMSSE across the 12 M5 hierarchy levels:

- Total
- State
- Store
- Category
- Department
- State/Category
- State/Department
- Store/Category
- Store/Department
- Item
- Item/State
- Item/Store

WRMSSE is calculated by aggregating train, actual, and predicted sales at each hierarchy level, scaling each series by its historical sales movement, weighting by recent dollar sales, and averaging the weighted RMSSE scores across levels.

## Large Files

Large data, pickle, model, and prediction files are tracked with Git LFS.

Install Git LFS before cloning or pulling the full project:

```bash
git lfs install
```

The raw M5 CSV files are stored as the original Kaggle archive:

```text
data/m5-forecasting-accuracy.zip
```

Extract this ZIP into `data/` before running notebooks from a fresh clone.

`pickles/train_cv1.pkl` is larger than GitHub's single-file LFS limit, so it is stored as split parts:

```text
pickles/train_cv1.pkl.part001
pickles/train_cv1.pkl.part002
pickles/train_cv1.pkl.part003
```

To rebuild it on Windows PowerShell:

```powershell
$parts = Get-ChildItem pickles/train_cv1.pkl.part* | Sort-Object Name
$out = [System.IO.File]::Create((Resolve-Path pickles).Path + "\train_cv1.pkl")
foreach ($part in $parts) {
    $bytes = [System.IO.File]::ReadAllBytes($part.FullName)
    $out.Write($bytes, 0, $bytes.Length)
}
$out.Close()
```
