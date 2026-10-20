# Supermarket Sales Analysis

Exploratory analysis of 1,000 supermarket invoices across three branches (Jan–Mar 2019): where sales come from, how they trend over time, which customer segments spend more, and what (if anything) drives customer ratings.

Everything is in one notebook: `Supermarket_Sales_Analysis.ipynb`.

## Questions answered

- Which branches and product lines bring in the most sales?
- How do sales change by month, weekday and hour of day?
- Do members, women or particular payment methods spend more per invoice?
- What explains customer ratings?

## Key findings

| Area | Result |
|---|---|
| Branches / products | Giza and *Food and beverages* lead, but the gaps are small and not statistically significant (p ≈ 0.8) |
| Trends | February was the weakest month (97k vs 116k in Jan, 109k in Mar). Saturday is the best weekday, Monday the weakest. Sales peak at 7 pm |
| Customers | Women spend more per invoice (≈341 vs ≈299, p < 0.01). Members spend ≈10% more, but this is only suggestive (p ≈ 0.08). Payment method makes no difference |
| Ratings | Average 6.97, spread evenly from 4 to 10. No significant link to branch, product, spend, customer type or payment method |

The data is very uniform, which is typical of simulated sample data. The "no difference" results hold for this dataset, but be careful about generalising from it.

## Data

`SuperMarket_Analysis.xlsx` has one row per invoice and 17 columns: invoice ID, branch, city, customer type, gender, product line, unit price, quantity, tax, sales, date, time, payment method, cogs, gross margin percentage, gross income and rating.

Notes from cleaning:

- **Dates:** the `Date` column mixes text (`M/D/YYYY`) with Excel dates whose day and month were swapped. The notebook repairs this; the corrected range is 1 Jan – 30 Mar 2019 (89 days).
- **Revenue:** `Unit price × Quantity` equals `cogs`, and `Sales` is that figure plus 5% tax. `Sales` is used as the headline measure.
- **Branches:** each branch maps to one city (Alex → Yangon, Cairo → Mandalay, Giza → Naypyitaw).
- No missing values; every invoice ID is unique.

## Getting started

```bash
git clone <your-repo-url>
cd <your-repo-name>
pip install -r requirements.txt
jupyter notebook Supermarket_Sales_Analysis.ipynb
```

Keep `SuperMarket_Analysis.xlsx` in the same folder as the notebook. Run all cells from the top.

## Method

- Pandas for cleaning and aggregation, Matplotlib for charts.
- Group differences are tested with non-parametric tests from SciPy (Kruskal–Wallis and Mann–Whitney U), since sales and ratings are not normally distributed. Rating vs sales uses Spearman correlation.

## Project structure

```
.
├── Supermarket_Sales_Analysis.ipynb   # analysis (outputs included)
├── SuperMarket_Analysis.xlsx          # dataset
├── requirements.txt
└── README.md
```

## Data source and licence

This looks like the public "Supermarket sales" sample dataset. Check the original source's licence before redistributing it, and add a `LICENSE` file for your own code.
