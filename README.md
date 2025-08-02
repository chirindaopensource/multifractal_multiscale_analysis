# README.md

# Market Complexity Dashboard: A Framework for Advanced Financial Time Series Analysis

<!-- PROJECT SHIELDS -->
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/python-3.9%2B-blue.svg)](https://www.python.org/downloads/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Imports: isort](https://img.shields.io/badge/%20imports-isort-%231674b1?style=flat&labelColor=ef8336)](https://pycqa.github.io/isort/)
[![Type Checking: mypy](https://img.shields.io/badge/type_checking-mypy-blue)](http://mypy-lang.org/)
[![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=flat&logo=numpy&logoColor=white)](https://numpy.org/)
[![SciPy](https://img.shields.io/badge/SciPy-%23025596?style=flat&logo=scipy&logoColor=white)](https://scipy.org/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=flat&logo=Matplotlib&logoColor=black)](https://matplotlib.org/)
[![Seaborn](https://img.shields.io/badge/Seaborn-%233776AB.svg?style=flat&logo=seaborn&logoColor=white)](https://seaborn.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-%23F37626.svg?style=flat&logo=Jupyter&logoColor=white)](https://jupyter.org/)
[![arXiv](https://img.shields.io/badge/arXiv-2507.23414-b31b1b.svg)](https://arxiv.org/abs/2507.23414)
[![Research](https://img.shields.io/badge/Research-Financial%20Complexity-green)](https://github.com/chirindaopensource/multifractal_multiscale_analysis)
[![Discipline](https://img.shields.io/badge/Discipline-Econophysics-blue)](https://github.com/chirindaopensource/multifractal_multiscale_analysis)
[![Methodology](https://img.shields.io/badge/Methodology-Nonlinear%20Time%20Series-orange)](https://github.com/chirindaopensource/multifractal_multiscale_analysis)
[![Year](https://img.shields.io/badge/Year-2025-purple)](https://github.com/chirindaopensource/multifractal_multiscale_analysis)

**Repository:** `https://github.com/chirindaopensource/multifractal_multiscale_analysis`

**Owner:** 2025 Craig Chirinda (Open Source Projects)

This repository contains an **independent**, professional-grade Python implementation of the research methodology from the 2025 paper entitled **"Complexity of Financial Time Series: Multifractal and Multiscale Entropy Analyses"** by:

*   Oday Masoudi
*   Farhad Shahbazi
*   Mohammad Sharifi

The project provides a complete, end-to-end computational framework for quantifying the dynamic complexity of financial assets. It moves beyond traditional, linear measures of risk (like standard deviation) to deliver a deeper, more nuanced characterization of market behavior based on concepts from information theory and fractal geometry. The goal is to provide a transparent, robust, and computationally efficient toolkit for researchers and practitioners to analyze nonlinearity, predictability, and the rich scaling structure of financial time series.

## Table of Contents

- [Introduction](#introduction)
- [Theoretical Background](#theoretical-background)
- [Features](#features)
- [Methodology Implemented](#methodology-implemented)
- [Core Components (Notebook Structure)](#core-components-notebook-structure)
- [Key Callable: market_complexity_dashboard_generator](#key-callable-market_complexity_dashboard_generator)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Input Data Structure](#input-data-structure)
- [Usage](#usage)
- [Output Structure](#output-structure)
- [Project Structure](#project-structure)
- [Customization](#customization)
- [Contributing](#contributing)
- [License](#license)
- [Citation](#citation)
- [Acknowledgments](#acknowledgments)

## Introduction

This project provides a Python implementation of the methodologies presented in the 2025 paper "Complexity of Financial Time Series: Multifractal and Multiscale Entropy Analyses." The core of this repository is the iPython Notebook `multifractal_multiscale_analysis_draft.ipynb`, which contains a comprehensive suite of functions to replicate the paper's findings, from initial data validation and cleansing to the final generation of complexity metrics, statistical tests, and publication-quality reports.

Traditional financial analysis often relies on the first two moments of the return distribution (mean and variance). However, these measures fail to capture the rich, nonlinear, and non-stationary dynamics that characterize modern financial markets. This project provides the tools to explore this hidden structure.

This codebase enables users to:
-   Rigorously validate, cleanse, and prepare financial time series data using a sophisticated, multi-stage protocol.
-   Quantify the irregularity and predictability of assets across dozens of time scales using Refined Composite Multiscale Sample Entropy (RCMSE).
-   Characterize the "fractal fingerprint" of an asset's volatility using Multifractal Detrended Fluctuation Analysis (MF-DFA).
-   Statistically test for the presence of significant nonlinear correlations by comparing results against a computationally generated null model (surrogate data).
-   Automatically generate a complete "complexity dashboard," including summary tables, scientific visualizations, and validation reports.

## Theoretical Background

The implemented methods are grounded in econophysics, a field that applies concepts from statistical physics and nonlinear dynamics to understand economic and financial systems.

**1. Refined Composite Multiscale Sample Entropy (RCMSE):**
Sample Entropy is a measure of the unpredictability or irregularity of a time series. It quantifies the conditional probability that two similar patterns of length `m` will remain similar when a new data point is added. A lower entropy implies more regularity and predictability. RCMSE extends this concept by:
-   **Multiscale Analysis:** Applying a "coarse-graining" procedure to analyze the series at different time scales (horizons), revealing how predictability changes from short-term to long-term.
-   **Refined Composite Method:** Using overlapping windows during coarse-graining to produce more stable and reliable entropy estimates, especially for the finite time series common in finance.
The final calculation is based on the logarithm of the ratio of aggregated pattern counts:
$$
\text{RCMSE}(x, \tau, m, r) = -\ln\left(\frac{\sum_{k=1}^{\tau} n^{m+1}_{(k,\tau)}}{\sum_{k=1}^{\tau} n^{m}_{(k,\tau)}}\right)
$$

**2. Multifractal Detrended Fluctuation Analysis (MF-DFA):**
Financial time series often exhibit multifractality, meaning their scaling properties (how volatility changes with the measurement scale) are not uniform but vary over time. MF-DFA is a powerful technique to quantify this phenomenon.
-   **Detrended Fluctuation:** The method systematically removes local trends from the data at different scales `s`, allowing for an accurate measurement of the underlying fluctuation dynamics.
-   **q-order Moments:** It calculates a `q`-dependent fluctuation function `F_q(s)` that magnifies either large (`q > 0`) or small (`q < 0`) fluctuations.
-   **Singularity Spectrum:** The final output is the singularity spectrum, `f(α)`. This spectrum is a "fingerprint" of the asset's complexity. The width of the spectrum, `Δα`, is a direct measure of the degree of multifractality: a wider spectrum implies a more complex, heterogeneous process with a richer mixture of behaviors.
$$
F_q(s) \sim s^{h(q)} \quad \xrightarrow{\text{Legendre Transform}} \quad (\alpha, f(\alpha))
$$

## Features

The provided iPython Notebook (`multifractal_multiscale_analysis_draft.ipynb`) implements the full research pipeline, including:

-   **Data Pipeline:** A robust validation and cleansing module that performs structural checks, advanced gap-filling, and outlier removal.
-   **High-Performance Analytics:** Elite-grade, vectorized implementations of RCMSE and MF-DFA using advanced NumPy features for maximum speed and memory efficiency.
-   **Statistical Rigor:** A parallelized surrogate data analysis framework to test the statistical significance of the complexity measures.
-   **Automated Orchestration:** A master function that runs the entire end-to-end workflow, from raw data to final reports, with a single call.
-   **Comprehensive Reporting:** Automated generation of publication-quality summary tables and scientific visualizations that replicate the key exhibits from the source paper.
-   **Built-in Quality Control:** An automated verification module to check the plausibility of results against theoretical expectations and known benchmarks.

## Methodology Implemented

The core analytical steps directly implement the methodology from the paper:

1.  **Data Validation and Preparation (Task 1):** The pipeline ingests raw price data, performs over a dozen structural and quality checks, and applies a sophisticated cleansing protocol including targeted gap-filling and outlier removal.
2.  **Preprocessing (Task 2):** It transforms clean prices into log-returns, calculates their key statistical moments, and generates a shuffled surrogate dataset for control analysis.
3.  **RCMSE Analysis (Task 3):** It computes the full RCMSE profile and total complexity score for each asset.
4.  **MF-DFA Analysis (Task 4):** It computes the generalized Hurst exponents and the full singularity spectrum (`α`, `f(α)`, `Δα`) for each asset.
5.  **Control Analysis (Task 5):** It runs the RCMSE and MF-DFA analyses on an ensemble of shuffled datasets in parallel to generate a null distribution for the complexity metrics.
6.  **Statistical Testing (Task 7):** It performs formal hypothesis tests (empirical p-values, z-scores) to determine if the complexity of the original data is statistically significant.
7.  **Reporting and Verification (Task 8):** It synthesizes all outputs into summary tables, plots, and a final verification report.

## Core Components (Notebook Structure)

The `multifractal_multiscale_analysis_draft.ipynb` notebook is structured as a logical pipeline with modular functions for each task:

-   **Task 1:** Data Validation and Cleansing (`validate_and_prepare_data`).
-   **Task 2:** Preprocessing and Characterization (`preprocess_and_characterize_data`).
-   **Task 3:** RCMSE Implementation (`compute_rcmse_profile`).
-   **Task 4:** MF-DFA Implementation (`compute_mfdfa_analysis`).
-   **Task 5:** Shuffling Control Analysis (`conduct_shuffling_analysis`).
-   **Task 6:** Primary Pipeline Orchestrator (`run_complexity_analysis_pipeline`).
-   **Task 7:** Robustness and Statistical Significance Testing.
-   **Task 8:** Output Generation, Verification, and Master Orchestrator.

## Key Callable: market_complexity_dashboard_generator

The central function in this project is `market_complexity_dashboard_generator`. It orchestrates the entire analytical workflow from raw data to a final, comprehensive report object.

```python
def market_complexity_dashboard_generator(
    df_prices: pd.DataFrame,
    study_config: Dict[str, Any],
    run_sensitivity: bool = False
) -> Dict[str, Any]:
    """
    Master orchestrator for the entire Market Complexity Dashboard framework.
    """
    # ... (implementation is in the notebook)
```

## Prerequisites

-   Python 3.9+
-   Core dependencies: `pandas`, `numpy`, `scipy`, `matplotlib`, `seaborn`.

## Installation

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/chirindaopensource/multifractal_multiscale_analysis.git
    cd multifractal_multiscale_analysis
    ```

2.  **Create and activate a virtual environment (recommended):**
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install Python dependencies:**
    ```sh
    pip install pandas numpy scipy matplotlib seaborn
    ```

## Input Data Structure

The pipeline requires two inputs passed to the `market_complexity_dashboard_generator` function:

1.  **`df_prices`**: A `pandas.DataFrame` where the index is a `DatetimeIndex` and columns are individual asset prices.
2.  **`study_config`**: A nested Python dictionary that controls all hyperparameters of the analysis. A fully specified example is provided in the notebook.

## Usage

The `multifractal_multiscale_analysis_draft.ipynb` notebook provides a complete, step-by-step guide. The core workflow is:

1.  **Prepare Inputs:** Load your asset prices into a DataFrame and define the `study_config` dictionary.
2.  **Execute Pipeline:** Call the master orchestrator function:
    ```python
    dashboard = market_complexity_dashboard_generator(
        df_prices=my_price_data_df,
        study_config=my_config
    )
    ```
3.  **Inspect Outputs:** Programmatically access any result from the returned `dashboard` dictionary. For example, to view the main MF-DFA summary table:
    ```python
    mdfa_summary_table = dashboard['summary_tables']['Table3_MFDFA_Spectrum_Widths']
    print(mdfa_summary_table)
    ```

## Output Structure

The `market_complexity_dashboard_generator` function returns a single, comprehensive dictionary with the following top-level keys:

-   `main_analysis_results`: A deeply nested dictionary containing all raw numerical results from the RCMSE, MF-DFA, and shuffling analyses.
-   `pipeline_validation_report`: A dictionary summarizing the results of the automated quality control checks.
-   `sensitivity_analysis_results`: A `pd.DataFrame` with the results of the parameter sensitivity analysis (if run).
-   `summary_tables`: A dictionary of `pd.DataFrame` objects, each representing a publication-quality summary table.
-   `figure_paths`: A dictionary mapping figure names to the file paths where they were saved.
-   `benchmark_verification_report`: A report detailing the comparison of key results against known benchmarks.

## Project Structure

```
multifractal_multiscale_analysis/
│
├── multifractal_multiscale_analysis_draft.ipynb  # Main implementation notebook   
├── requirements.txt                              # Python package dependencies
├── LICENSE                                       # MIT license file
└── README.md                                     # This documentation file
```

## Customization

The pipeline is highly customizable via the master `study_config` dictionary. Users can easily modify:
-   The `embedding_dimension_m` and `tolerance_r_factor` for RCMSE.
-   The `q_range` and `polynomial_order` for MF-DFA.
-   The `time_series_length` and `study_end_date` to change the analysis window.
-   The `parameter_grid` in the `run_parameter_sensitivity_analysis` function to test different hyperparameters.

## Contributing

Contributions are welcome. Please fork the repository, create a feature branch, and submit a pull request with a clear description of your changes. Adherence to PEP 8, type hinting, and comprehensive docstrings is required.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Citation

If you use this code or the methodology in your research, please cite the original paper:

```bibtex
@article{masoudi2025complexity,
  title={Complexity of Financial Time Series: Multifractal and Multiscale Entropy Analyses},
  author={Masoudi, Oday and Shahbazi, Farhad and Sharifi, Mohammad},
  journal={arXiv preprint arXiv:2507.23414},
  year={2025}
}
```

For the implementation itself, you may cite this repository:
```
Chirinda, C. (2025). A Python Implementation of "Complexity of Financial Time Series: Multifractal and Multiscale Entropy Analyses". 
GitHub repository: https://github.com/chirindaopensource/multifractal_multiscale_analysis
```

## Acknowledgments

-   Credit to Oday Masoudi, Farhad Shahbazi, and Mohammad Sharifi for their clear and insightful research.
-   Thanks to the developers of the scientific Python ecosystem (`numpy`, `pandas`, `scipy`, `matplotlib`) that makes this work possible.

--

*This README was generated based on the structure and content of `multifractal_multiscale_analysis_draft.ipynb` and follows best practices for research software documentation.*
