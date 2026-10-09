# Optimizing the U.S. Energy Mix to Reduce Greenhouse Gas Emissions by 2030

## Project Overview

This applied mathematics capstone project investigates the relationship between the composition of the U.S. energy mix and greenhouse gas emissions. It combines historical data analysis, Ridge regression, and linear programming to explore how different energy sources affect emissions intensity and identify a possible energy mix for 2030.

The project has two main objectives:

1. Examine the statistical relationship between energy-source composition and greenhouse gas emissions intensity in the United States.
2. Determine an energy mix that minimizes projected 2030 emissions while satisfying energy demand, capacity bounds, grid-stability requirements, and other practical constraints.

## Research Question

**What is the statistical relationship between energy source composition and greenhouse gas emission intensity in the United States., and what is the
optimal energy mix that minimizes emissions by 2030 under projected demand trends?**

## Data Sources

The analysis combines information from several sources:

- [Our World in Data Energy Mix](https://ourworldindata.org/energy-mix) — historical primary energy consumption by source
- [Climate Watch Historical GHG Emissions](https://www.climatewatchdata.org/ghg-emissions) — historical U.S. greenhouse gas emissions
- [U.S. Energy Information Administration Annual Energy Outlook 2025](https://www.eia.gov/outlooks/aeo/) — projected 2030 energy demand
- Lifecycle-emission estimates from the IPCC, UNECE, World Nuclear Association, and other energy research sources

The final historical dataset covers the period from 1965 through 2023.

## Project Workflow

### 1. Data Preparation

- Extracted U.S. energy and emissions data from multiple sources
- Merged and cleaned the historical datasets
- Converted energy consumption into percentage shares by source
- Calculated annual emissions intensity in tCO₂e/TWh
- Examined missing values, inconsistent records, and predictor relationships
- Removed Biofuels and Other Renewables from the regression model after evaluating multicollinearity and coefficient stability

### 2. Regression Diagnostics

A multiple linear regression model was initially considered. Diagnostic testing included:

- Correlation analysis
- Variance Inflation Factor analysis
- Ramsey RESET testing
- Residual-versus-predicted plots
- Comparison of multiple linear regression and Ridge coefficients

The diagnostic results supported a linear relationship but revealed substantial multicollinearity among the energy-share predictors.

### 3. Ridge Regression

Ridge regression was selected because it reduces coefficient instability caused by correlated predictors while retaining all included variables.

The final model uses seven predictors:

- Solar
- Wind
- Hydropower
- Nuclear
- Natural gas
- Oil
- Coal

The model evaluates their relationships with historical U.S. emissions intensity.

### 4. Linear Programming

A linear programming model was developed with PuLP to minimize projected 2030 lifecycle emissions.

The model includes:

- Projected 2030 energy demand
- Lifecycle emission factors for each energy source
- Lower and upper bounds based on historical growth and model results
- A minimum baseload requirement
- Limits on intermittent solar and wind generation
- A fossil-fuel share constraint
- A model-adjusted emissions-reduction target

Several scenarios were evaluated, including:

1. Current lifecycle-emission factors without carbon capture and storage
2. Current lifecycle-emission factors with increased renewable-energy storage
3. Carbon capture and storage applied to fossil-fuel lifecycle emissions
4. Carbon capture and storage combined with increased renewable-energy storage

### 5. Sensitivity Analysis

Sensitivity testing examined how model feasibility changed when modifying:

- Fossil-fuel lifecycle emissions
- Solar and wind upper bounds
- Natural gas, oil, and coal lower bounds
- Hydropower upper bounds
- Emissions-reduction targets
- Ridge regularization strength

## Key Results

### Ridge Regression

- The Ridge model achieved an in-sample R² of approximately **0.988**.
- Nuclear, solar, wind, and hydropower were negatively associated with emissions intensity.
- Coal, oil, and natural gas were positively associated with emissions intensity.
- Coal showed the strongest positive association with emissions intensity.
- Nuclear showed the strongest negative association among the included predictors.

### Linear Programming

Under the defined bounds and current lifecycle-emission factors, the model could not achieve the targeted 50% emissions reduction.

A feasible solution became possible when fossil-fuel lifecycle-emission factors were adjusted to represent carbon capture and storage.

The resulting energy mix was:

| Energy Source | Optimal Share |
|---|---:|
| Solar | 13.00% |
| Wind | 12.00% |
| Hydropower | 0.05% |
| Nuclear | 15.00% |
| Natural Gas | 32.95% |
| Oil | 20.00% |
| Coal | 0.00% |
| Other Renewables | 7.00% |

This scenario produced approximately **2.68 billion tCO₂e** in model-estimated lifecycle emissions.

Increasing the allowable solar and wind share under an expanded-storage scenario reduced estimated emissions further, to approximately **2.53 billion tCO₂e**.

These results represent modeled scenarios rather than forecasts. They demonstrate how the optimal solution changes under the assumptions and constraints included in the model.

## Tools and Skills

- Python
- Jupyter Notebook
- Visual Studio Code
- Microsoft Excel
- Pandas
- NumPy
- Scikit-learn
- Statsmodels
- PuLP
- Matplotlib
- Seaborn
- Data cleaning and integration
- Feature engineering
- Regression diagnostics
- Ridge regression
- Hyperparameter tuning
- Linear programming
- Constraint development
- Sensitivity analysis
- Data visualization
- Mathematical modeling

## Limitations

- Energy-share predictors are structurally related because their percentages sum to 100%.
- Ridge regression reduces coefficient instability but does not eliminate the underlying dependence among predictors.
- The reported R² and error measures describe the model’s fit to the historical dataset.
- Lifecycle-emission estimates vary across studies and depend on technology and system boundaries.
- The linear programming model assumes constant lifecycle-emission factors through 2030.
- The optimization does not directly incorporate financial costs, infrastructure construction, political feasibility, or regional resource availability.
- Feasible carbon-capture scenarios assume that the technology can be deployed at a sufficiently large scale.
- The 35% adjustment used to estimate the 2005 lifecycle-emissions baseline is a simplifying modeling assumption.
- Optimization results are sensitive to the selected bounds and constraints.

## Repository Contents

- [`U.S. Energy Mix Analysis.ipynb`](U.S.%20Energy%20Mix%20Analysis.ipynb) — data preparation, Ridge regression, linear programming, sensitivity analysis, and visualizations
- [`1965_2023_Data_USA.csv`](1965_2023_Data_USA.csv) — prepared historical dataset used in the analysis
- [`Optimizing the U.S. Energy Mix Report.pdf`](Optimizing%20the%20U.S.%20Energy%20Mix%20Report.pdf) — complete written report with methodology, results, references, and appendices

## Acknowledgement

This project was originally completed as the final project for an Applied Mathematics classs and was later reviewed and revised for portfolio presentation.
