# Financial Data Preprocessing from WRDS

_Last updated: April 5, 2025_

> 🚧 This is a work in progress. The current version includes initial data extraction and preprocessing but does not represent the final version of the project.

This repository contains two Jupyter Notebooks that extract, clean, and preprocess financial datasets from WRDS (Wharton Research Data Services), focusing primarily on CRSP and Compustat data. The ultimate goal is to prepare datasets for empirical asset pricing or corporate finance research.

---

## Files

### `Data.ipynb`

This notebook connects to the WRDS database and pulls monthly stock return and firm data from CRSP and Compustat. Key steps include:

- **WRDS Connection Setup**: Uses `wrds` Python package to connect securely.
- **CRSP Monthly Data Extraction**: 
  - Downloads monthly return data (`ret`, `retx`) and other firm-level information (price, shares outstanding, exchange code, etc.).
  - Adjusts returns to account for delisting returns (`dlret`), filling in missing values with a conservative estimate of -0.5.
  - Adds `YearMonth` variable aligned to month-end for easier merging with other datasets.
  - Saves the cleaned data as a `.parquet` file.

### `Preprocess.ipynb`

This notebook loads and merges the cleaned CRSP data and continues with further processing:

- **Market Equity Calculation**:
  - Computes market equity (`ME = |PRC| × SHROUT`) and aligns pricing and return variables for forward return calculation.
- **Return Forecast Variables**:
  - Generates key variables such as lagged price and forward return (`bh1m`), setting up the structure for return prediction models or portfolio sorting.
- **Data Cleaning**:
  - Filters duplicates and ensures correct sorting by `permno` and `YearMonth`.

---

## Requirements

The code depends on the following packages:

- `pandas`
- `numpy`
- `wrds`
- `pyarrow`
- `matplotlib`
- `tqdm`

Make sure you have access to WRDS with valid credentials to run the data extraction cells.

---

## Output

Processed datasets are saved in `.parquet` format under the `./data/WRDS/` directory.

---

## Notes

This project is under active development and more modules will be added in future versions (e.g., IBES data processing, fundamental signals, portfolio construction, etc.).
