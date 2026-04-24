# Metal Prices in Transition: Structural Tightness and the Long-Term Outlook for Copper and Silver

## Overview

This repository contains the paper, poster, progress presentation, data, figures, and code for our project on metal-price dynamics. The project asks whether copper and silver are becoming structurally tighter than other major metals, and whether that tightening shows up in both historical price data and physical-market evidence.

## Motivation

Metal prices respond to both short-run macro conditions and longer-run supply and demand pressure. Copper matters because it sits at the center of electrification, grid expansion, construction, and infrastructure. Silver is useful because it behaves partly like a precious metal and partly like an industrial input used in electronics and solar PV. Looking at both together makes it possible to study macro sensitivity and structural tightness in the same project.

## Data

The project combines historical monthly price data with macro controls and metal-specific structural inputs.

### Historical price and macro data
- World Bank Pink Sheet monthly prices for oil, aluminum, copper, nickel, zinc, gold, and silver
- FRED series for the broad U.S. dollar, VIX, the 10Y-2Y yield spread, unemployment, and the S&P 500
- OECD industrial production growth
- LME copper stocks

### Structural market inputs
- IEA copper demand outlook
- ICSG copper balance releases
- Silver Institute demand and supply releases
- USGS mineral summaries

The main comparison set includes aluminum, copper, nickel, zinc, gold, and silver.

## Code and analysis workflow

The coding side of the project was built to do more than just load a final spreadsheet. The notebook rebuilds the main monthly regression panel from the raw source files and then reproduces the figures used in the paper, poster, and slide deck.

### What the code does
- reads the raw CSV files and standardizes date fields to a monthly index
- aggregates daily VIX and yield-spread data to monthly averages
- merges monthly prices with macro controls, unemployment, OECD industrial production growth, and copper inventory data
- computes log returns, month-over-month changes, lagged variables, and indexed price series
- checks for duplicate rows, missing values in the core modeling tables, and sample-window consistency
- re-estimates the expanded HAC regressions for each metal
- estimates a separate copper inventory model using LME stock changes
- plots the historical figures, structural copper and silver figures, and long-run Monte Carlo bands

### Data quality checks
The repository includes **12 raw source files** and **6 processed analysis tables**. The long metal panel contains **1,878 metal-month observations** from **2000-02 to 2026-02** with nealry no duplicate rows or missing cells. The regression panel rebuilt from raw macro and price data spans **2010-01 to 2025-12**, and after lags and month-over-month changes are constructed, the expanded HAC models are estimated on **189 monthly observations** for each metal.

### Main tools
- `pandas` for cleaning and merging
- `numpy` for transformations and simulation inputs
- `matplotlib` for all figures
- `statsmodels` for the HAC regressions

The HAC specification is important because it makes the monthly regressions more reliable in the presence of serial correlation and changing volatility, which are common in commodity returns.

## Main results

Two results stand out in the project.

1. The broad U.S. dollar is a strong negative driver across the six-metal panel in the expanded monthly regressions.
2. Physical-market evidence points to tighter conditions in copper and silver. Copper inventories fell sharply during 2025, while silver demand remained above supply and industrial demand stayed elevated.

<p align="center">
  <img src="./figures/Project%20Summary%20Figure.png" alt="Summary figure showing broad dollar coefficients, copper price versus LME stocks, and silver demand versus supply" width="980">
</p>

<p align="center"><em>Figure 1. Summary of the main empirical results. The left panel shows that the broad U.S. dollar enters negatively across all six metals in the expanded HAC regressions. The middle panel shows that copper prices stayed firm while LME stocks fell, which is consistent with tighter exchange availability. The right panel shows that silver demand remained above supply in 2024 and in the latest 2025 estimate, reinforcing the idea that silver is both a monetary and industrial metal.</em></p>

## Repository contents

- `paper/` final paper in PDF and Word format
- `slides/` progress presentation
- `poster/` research poster
- `notebooks/` main analysis notebook
- `figures/` exported figures used across the project
- `data/raw/` source files used in the project
- `data/processed/` cleaned datasets used in the notebook and main figures
- `docs/Data Dictionary.csv` variable descriptions for the included datasets

