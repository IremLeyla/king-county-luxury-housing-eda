# Buy Loud: Luxury Housing in King County 🏡

An exploratory data analysis of 21,597 home sales in King County, WA (Seattle area), from May 2014 to May 2015. We set out to find what really drives house prices and to build a shortlist of homes for one specific client.

Built by **Dhanya** ([@Dhanyacode12](https://github.com/Dhanyacode12)) and **Irem** ([@IremLeyla](https://github.com/IremLeyla)) as part of the AI Project Management bootcamp at neue fische.

📊 **[View the presentation (PDF)](EDA_Presentation/EDA_Project_Dhanya_Irem_2026.pdf)**

---

## The client

**Jennifer Montgomery** is a high-budget buyer looking for a statement property. She wants to buy within a month and resell within a year, so her choice needs to combine prestige with strong resale potential.

We translated her wishes into data filters:

| What she asked for | What that means in the data |
| --- | --- |
| High budget, wants to show off | `price` ≥ 90th percentile |
| Waterfront access | `waterfront = 1` |
| Renovated | `yr_renovated > 0` |
| High grade | `grade > 10` |

## Hypotheses and findings

**H1: Location and grade interact to drive top-tier prices.** ✅ Confirmed.
Price rises with grade in every one of the top 10 zip codes, but how much it rises depends on location. In premium zip codes such as 98115 and 98006, grade 12+ homes reach median prices of $2.3M to $2.65M. In zip codes such as 98042 and 98023, the same grade stays under $750K.

**H2: Waterfront access commands a price premium.** ✅ Confirmed.
The median waterfront home sells for about $1.5M, roughly 3x the median non-waterfront home (about $450K). However, the single most expensive sales in the dataset are not waterfront, so it is a strong premium rather than the only path to a top price.

**H3: Renovation lifts price.** ✅ Confirmed.
Renovated homes have a median price of about $608K compared with $448K for non-renovated homes, roughly 36% more. The two most expensive sales in the whole dataset are renovated homes.

**Beyond the hypotheses**, a correlation analysis across all numeric features showed that living space (`sqft_living`, r = 0.70), grade (r = 0.67), and above-ground living space (`sqft_above`, r = 0.61) are the strongest single predictors of price.

## Resale potential

Because Jennifer plans to resell within a year, we looked at the 176 houses that sold more than once in the dataset. All of them resold within a year, 94.9% sold for more than their original price, and the median gain was 54.4%.

> **Caveat:** This is a small sample, and quick resales are often bought cheaply and renovated before being sold again ("flips"). These numbers describe that group, not typical appreciation across the whole market.

## The shortlist

We gave every house a `match_score` from 0 to 4 based on how many of Jennifer's criteria it meets. Only **4 houses** in the entire dataset match all four. The top three by price are:

| Rank | Price | Zip code | Living space (sqft) | Year built | Bedrooms |
| --- | --- | --- | --- | --- | --- |
| #1 | $7.1M | 98004 | 10,040 | 1940 | 5 |
| #2 | $4.7M | 98040 | 9,640 | 1983 | 5 |
| #3 | $3.3M | 98008 | 4,220 | 1958 | 3 |

The notebook shows these on an interactive map.

## Data cleaning highlights

- Converted `date` to a proper datetime and recast `zipcode`, `condition`, and `grade` as text or categories rather than numbers.
- Fixed renovation years that were stored 10x too large in the database (for example `19950` instead of `1995`).
- Analysed missing values in `yr_renovated`, `waterfront`, `sqft_basement`, and `view`, and kept unknown waterfront status as its own group instead of guessing.

## Repository structure

| File / Folder | Description |
| --- | --- |
| `04_eda.ipynb` | The main analysis notebook: cleaning, hypotheses, correlations, resale analysis, and the client shortlist |
| `03_fetching_the_data_eda.ipynb` | Connects to the PostgreSQL database and loads the joined dataset into pandas |
| `EDA_Presentation/` | The final client presentation (PDF) |
| `column_names.md` | Data dictionary for the King County dataset |
| `01_assignment.md`, `02_workflow.md` | The original project brief and recommended workflow from the bootcamp |

## Tools

Python 3.13, pandas, matplotlib, seaborn, plotly, SQLAlchemy, psycopg2, and PostgreSQL, with dependencies managed by [uv](https://github.com/astral-sh/uv).

## Running it yourself

The data was loaded from a PostgreSQL database provided by the bootcamp, so the notebooks can't be re-run without access credentials.
## Acknowledgements

Project brief and template by [neue fische](https://www.neuefische.de/). Dataset: King County House Sales, 2014–2015.
