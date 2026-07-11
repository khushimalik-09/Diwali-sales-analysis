# Diwali Sales Analysis

Exploratory data analysis and statistical hypothesis testing on Diwali sales transaction data (11,251 records) to identify buyer patterns and validate which of those patterns are statistically real vs. driven by sample size / volume.

## Project Overview

This project goes beyond descriptive charts by adding formal hypothesis testing to check whether the visual patterns from EDA actually hold up statistically — a step that's often skipped but changes the business conclusions significantly.

**Workflow:** Data Cleaning → Exploratory Data Analysis → Hypothesis Testing → Business Conclusion

## Dataset

- **Source:** Diwali Sales Data (`Diwali Sales Data.csv`)
- **Size:** 11,251 transactions, 15 columns
- **Key fields:** `Gender`, `Age Group`, `Age`, `Marital_Status`, `State`, `Zone`, `Occupation`, `Product_Category`, `Orders`, `Amount`

## Tech Stack

- **Python** — pandas, numpy
- **Visualization** — matplotlib, seaborn
- **Statistical Testing** — scipy.stats, statsmodels

## Data Cleaning

- Dropped irrelevant columns (`Status`, `unnamed1`)
- Removed rows with missing values
- Cast `Amount` to integer type
- Verified no duplicate records

## Exploratory Data Analysis

Analyzed buyer behavior and total spend across:
- Gender
- Age Group
- State (top 10 by orders and revenue)
- Marital Status × Gender
- Occupation
- Product Category

**Initial (descriptive) findings:** Highest *total* spend came from married women, aged 26-35, based in Uttar Pradesh / Maharashtra / Karnataka, working in IT / Healthcare / Aviation, buying Food / Clothing / Electronics.

## Hypothesis Testing

EDA shows totals — which are heavily influenced by how many buyers are in each group. To check whether these were real per-person effects or just volume effects, three statistical tests were run:

| Test | Comparison | p-value | Significant? | Takeaway |
|---|---|---|---|---|
| Independent t-test (Welch's) | Gender vs. Amount | 0.2461 | No | Per-person spend is statistically equal across genders |
| One-way ANOVA + Tukey HSD | Age Group vs. Amount | 0.0023 | Yes | 18-25 spends significantly less than 36-45 & 51-55 |
| Chi-square test of independence | Marital Status vs. Gender | 0.2066 | No | Marital status and gender are statistically independent |

**Key correction to the EDA-only view:** the higher *total* spend from female and married buyers is a volume effect (more buyers in that segment), not a higher spend per person. The one statistically defensible per-person effect is age — buyers aged **18-25 spend significantly less per transaction** than the 36-45 and 51-55 groups.

## Business Conclusion

- **For reach-driven campaigns:** target the 26-35 / married-women segments — that's where transaction volume concentrates.
- **For spend-per-customer campaigns:** don't assume gender or marital status move the needle — they don't, statistically. Age is the validated lever, with 18-25 customers representing the clearest upsell opportunity.

## Project Structure

```
├── Diwali_Sales_Analysis.ipynb   # Full notebook: cleaning, EDA, hypothesis testing, conclusion
├── Diwali Sales Data.csv         # Raw dataset (not included in repo)
└── README.md
```

## How to Run

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels
jupyter notebook Diwali_Sales_Analysis.ipynb
```

## Skills Demonstrated

- Data cleaning & preprocessing
- Exploratory data analysis & visualization
- Hypothesis testing (t-test, ANOVA, chi-square) and A/B testing methodology
- Statistical interpretation and translating results into business recommendations
