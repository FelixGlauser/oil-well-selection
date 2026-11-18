# Oil Well Selection — Profitability and Risk Analysis

## Project Overview

This project was developed as part of the TripleTen Data Science Bootcamp.

The oil company OilyGiant wants to identify the most profitable region for developing 200 new oil wells.

Three regions are analyzed using historical geological data. A Linear Regression model is trained for each region to predict oil reserves. The project then evaluates potential profitability and uses bootstrapping to assess financial risk.

**The key finding:** The region that initially appeared to be the most profitable was not the best investment choice after risk analysis.

## Business Objective

The objective is to recommend the region that offers the highest expected profit while keeping the probability of financial loss below 2.5%.

Business conditions:

- Development budget: $100 million
- Number of wells to develop: 200
- Revenue per product unit (1,000 barrels): $4,500
- Maximum acceptable probability of loss: 2.5%

## Dataset

Three datasets were provided, one for each region.

Each dataset contains 100,000 observations and the following variables:

- `id`: Unique well identifier
- `f0`, `f1`, `f2`: Geological features
- `product`: Volume of oil reserves

No missing values or duplicate rows were found.

The original datasets are not included in this repository.

## Project Workflow

### 1. Data Preparation and Exploration

- Loaded and inspected all three regional datasets.
- Checked for missing values and duplicate records.
- Analyzed descriptive statistics and reserve distributions.

### 2. Model Development

- Trained a Linear Regression model for each region.
- Split the data into 75% training and 25% validation sets.
- Evaluated predictions using RMSE and mean predicted reserves.

### 3. Initial Profitability Assessment

- Calculated the minimum reserve volume required per well to cover the investment.
- Selected the 200 wells with the highest predicted reserves in each region.
- Calculated potential profit using the actual reserve volumes of the selected wells.

### 4. Risk Analysis Using Bootstrapping

- Generated 1,000 bootstrap samples of 500 wells with replacement.
- Selected the 200 wells with the highest predicted reserves in each sample.
- Calculated the resulting profit distribution.
- Evaluated mean profit, 95% confidence intervals, and probability of financial loss.

## Model Evaluation

The Linear Regression models produced the following results:

| Region | Mean Predicted Reserves | RMSE |
|---|---:|---:|
| Region 0 | 92.59 | 37.58 |
| Region 1 | 68.73 | 0.89 |
| Region 2 | 94.97 | 40.03 |

Region 2 had the highest mean predicted reserve volume, while Region 1 had by far the lowest RMSE.

## Initial Profitability Results

Based on the 200 wells with the highest predicted reserves in each region:

| Region | Initial Potential Profit |
|---|---:|
| Region 0 | $33.21 million |
| Region 1 | $24.15 million |
| Region 2 | $27.10 million |

At this stage, Region 0 appeared to be the most attractive investment.

However, this initial result did not account for the uncertainty of the estimates or the probability of financial loss.

## Bootstrap Risk Analysis

The bootstrap analysis produced the following results:

| Region | Mean Profit | 95% Confidence Interval | Loss Risk |
|---|---:|---:|---:|
| Region 0 | $3.96 million | -$1.11M to $9.10M | 6.90% |
| Region 1 | $4.56 million | $0.34M to $8.52M | **1.50%** |
| Region 2 | $4.04 million | -$1.63M to $9.50M | 7.60% |

Only Region 1 meets the requirement of keeping the probability of loss below 2.5%.

It also achieves the highest mean profit among the eligible regions.

## Final Recommendation

The initial profitability assessment suggested Region 0 as the best option, with a potential profit of approximately $33.21 million.

The bootstrap analysis changed this conclusion:

- Region 0 has a loss risk of 6.90%.
- Region 2 has a loss risk of 7.60%.
- Region 1 has a loss risk of only 1.50% and the highest mean profit of approximately $4.56 million.

**Final decision: Region 1 is the recommended region for development.**

This project demonstrates why investment decisions should not be based on a single prediction or metric. Considering uncertainty, confidence intervals, and financial risk can fundamentally change the initial recommendation.

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Jupyter Notebook
- Linear Regression
- Bootstrapping
- Statistical Risk Analysis

## Key Skills Demonstrated

- Data preparation and exploratory data analysis
- Regression modeling
- Model evaluation using RMSE
- Profitability calculations
- Bootstrap simulation
- Confidence interval estimation
- Financial risk assessment
- Data-driven business decision-making
