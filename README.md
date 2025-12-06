# Bradford_Jones_Pref_Performance
# PI–TI Correlation, Nonlinearity, and Bayesian Model Comparison

This project analyzes how **Preference Index (PI)** — operationalized as ChatbotArena Elo — relates to several **Task Index (TI)** benchmarks, including ARC-AGI-2, MMLU, GPQA Diamond, SWE_Bench, and AIME.  
The workflow includes rank correlations, spline and piecewise regressions, bootstrap confidence intervals, and Bayesian WAIC model comparison.

---

## 1. Environment Setup

### Python Version
- Python **3.10+** (tested in Colab and locally)

### Install Dependencies
Create a `requirements.txt`:

numpy
pandas
scipy
matplotlib
seaborn
statsmodels
patsy
pymc
arviz

go
Copy code

Install:

```bash
pip install -r requirements.txt
In Google Colab, only PyMC needs explicit install:

python
Copy code
!pip install pymc arviz
2. Required Dataset
Place the dataset in the working directory:

Copy code
Frontier_Model_Outcomes_v1600.csv
The script automatically handles:

converting percent strings (e.g., "91.2%" → 91.2)

renaming model column

cleaning Elo values

standardizing PI (PI_z)

Expected columns include:

Unnamed: 0 (model name)

ChatbotArena_Elo

AIME (no tools)

GPQA Diamond

ARC-AGI-2

MMLU

SWE_Bench

3. Running the Analysis
In Google Colab
Upload the CSV: Fronteir_Model_Outcomes_vDeploy (included in Github Repository)

python
Copy code
from google.colab import files
files.upload()
Then run the full script as-is.

Locally
bash
Copy code
python analyze.py
4. Outputs
4.1 Correlation Analysis
Spearman ρ and Kendall τ between Elo and each benchmark

Bootstrap 95% confidence intervals

Scatter plots with regression lines

4.2 Nonlinear Modeling
Adaptive-degree cubic spline regression

Piecewise linear regression with data-driven knot selection

Plots of spline fits, piecewise fits, and bootstrap envelopes

4.3 Bayesian Comparison (PyMC)
Bayesian linear and spline regression models

WAIC computed per bootstrap sample

Probability the spline model outperforms linear (lower WAIC)

If dataset size is small (e.g., 5 models), the script automatically skips unstable bootstrap samples.

5. Repository Structure
pgsql
Copy code
.
├── Bradford_Jones_Pref_Performance (Code created for analysis)
├── Frontier_Model_Outcomes_vDeploy.csv
├── README.md

6. Runtime & Compute Requirements
Correlation + regressions: seconds

Bootstrap spline/piecewise (2000 iters): 1–3 minutes

Bayesian WAIC bootstrap (25 iters): 2–5 minutes

Memory footprint: <1 GB

No GPU required

7. Notes
Spline degrees are automatically reduced if the dataset is too small to avoid singular fits.

Expected numerical warnings (e.g., from tiny bootstrap samples) are suppressed for clarity.

Bayesian model comparison is included for completeness but benefits from larger datasets.
