# Temporal Renormalization of Persistent Macro-Risk Dynamics

This repository contains the analysis code for the paper

**Temporal Renormalization of Persistent Macro-Risk Dynamics Generates Effective Default Correlation**

by Shintaro Mori.

The purpose of this repository is to provide a minimal executable workflow for the main analyses in the paper. The empirical default data used in the paper are not included because they are derived from proprietary historical default datasets and cannot be redistributed.

## Repository structure

```text
temporal-renormalization-default-risk/
  README.md
  LICENSE
  requirements.txt

  data_synthetic/
    synthetic_monthly_defaults.csv
    synthetic_annual_defaults.csv

  notebooks/
    03_ou_binomial_temporal_renormalization.ipynb
    04_direct_and_renormalized_residual_fitting.ipynb

  figures/
    .gitkeep

  tables/
    .gitkeep
````

## Notebooks

### `03_ou_binomial_temporal_renormalization.ipynb`

This notebook reproduces the Section II workflow of the paper:

* construction of non-overlapping temporally aggregated default counts;
* empirical variance scaling of the monthly-equivalent default rate;
* Bayesian estimation of the monthly OU--Binomial state-space model;
* temporal coarse graining of posterior default-risk paths;
* posterior predictive variance decomposition;
* autocorrelation diagnostics;
* effective mixing distributions induced by temporal renormalization.

### `04_direct_and_renormalized_residual_fitting.ipynb`

This notebook reproduces the Section III workflow of the paper:

* direct fitting of OU--Binomial, OU--Davis--Lo, and OU--Vasicek models at each aggregation scale;
* covariance-share diagnostics for residual same-period dependence;
* WAIC and per-block elpd comparisons;
* renormalized fitting conditional on coarse-grained posterior risk paths;
* residual-parameter diagnostics for the OU--Davis--Lo and OU--Vasicek extensions;
* generation of the summary tables and figures used in Section III and the appendices.

## Data availability

The empirical default data analyzed in the paper are not included in this repository. They are derived from proprietary historical default datasets and therefore cannot be publicly shared.

The repository includes independently generated low-fidelity synthetic data in `data_synthetic/`. These synthetic data are provided only to make the notebooks executable and to demonstrate the analysis workflow. They are not derived from, fitted to, or calibrated to the proprietary empirical default data used in the paper.

Results obtained from the synthetic data are not intended to reproduce the empirical results reported in the paper.

Researchers with access to comparable default-count data can reproduce the empirical workflow by replacing the synthetic files with their own data files having the same column structure.

## Synthetic data format

The notebooks expect monthly and annual default-count data with the following basic structure.

### Monthly data

A monthly data file should contain at least:

```text
date, L, n
```

where:

* `date` is the monthly date;
* `L` is the number of defaults in that month;
* `n` is the corresponding number of obligors.

### Annual data

An annual data file should contain at least:

```text
year, source, L, n
```

where:

* `year` is the calendar year;
* `source` identifies the annual benchmark series;
* `L` is the number of defaults in that year;
* `n` is the corresponding number of obligors.

If the notebooks use different file names internally, the files in `data_synthetic/` should be renamed or the path settings in the notebooks should be edited accordingly.

## Installation

The code was developed in Python. A typical environment can be prepared with:

```bash
pip install -r requirements.txt
```

The main packages used are:

* `numpy`
* `pandas`
* `scipy`
* `matplotlib`
* `pymc`
* `arviz`
* `statsmodels`
* `jupyter`

Depending on the local environment, installation of `pymc` may require additional backend dependencies.

## Running the analysis

After installing the required packages, start Jupyter and run the notebooks in order:

```bash
jupyter notebook
```

Recommended order:

1. `notebooks/03_ou_binomial_temporal_renormalization.ipynb`
2. `notebooks/04_direct_and_renormalized_residual_fitting.ipynb`

The notebooks write generated figures and tables to the `figures/` and `tables/` directories.

## Reproducibility note

The Bayesian analyses use Markov chain Monte Carlo sampling. Small numerical differences may occur across platforms, package versions, and random seeds. The synthetic data are intended for workflow testing only; the numerical values obtained from them should not be compared with the empirical results in the paper.

## Citation

If you use this code, please cite the paper:

```text
Shintaro Mori,
Temporal Renormalization of Persistent Macro-Risk Dynamics Generates Effective Default Correlation,
2026.
```

## License

This repository is released under the MIT License. See `LICENSE` for details.


