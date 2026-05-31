![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![Python](https://img.shields.io/badge/Python-3.13.5-blue)
![License](https://img.shields.io/badge/License-Academic-lightgrey)

# Data Science Programming Project
## Analysing Ethnicity, Stop & Search, Prosecutions and Convictions in the UK
### Open Government Datasets — data.gov.uk

> **Key Finding:** Black individuals are stopped by police at 4 to 9.5 times the rate of White individuals per 1,000 population — and this disproportionality *worsened* after 2014 even as total stop and search volumes fell. Despite this, each stop of a Black individual is more likely to result in prosecution than a stop of a White individual, raising fundamental questions about the targeting, consistency, and fairness of stop and search practices in the UK.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Datasets Used](#datasets-used)
3. [Repository Structure](#repository-structure)
4. [How to Run](#how-to-run)
5. [Methodology](#methodology)
6. [Analysis and Findings](#analysis-and-findings)
7. [Conclusions](#conclusions)
8. [Limitations](#limitations)
9. [Recommendations](#recommendations)
10. [Libraries Used](#libraries-used)
11. [References](#references)
12. [Author](#author)

---

## Project Overview

This project analyses relationships between ethnic population distribution, stop and search activity, and criminal justice outcomes (prosecutions and convictions) across different regions, time periods, age groups, and offence types in England and Wales. Three open government datasets from data.gov.uk are combined to draw cross-dataset inferences about the UK criminal justice system.

The project introduces a computed **conviction rate** metric (convictions / prosecutions × 100), a **stop-to-prosecution efficiency ratio**, and a **Black:White disproportionality ratio** for stop and search — none of which are present in the raw datasets but which substantially deepen the analysis.

---

## Datasets Used

All datasets are publicly available from [data.gov.uk](https://www.data.gov.uk):

| Dataset | Coverage | Key Fields |
|---|---|---|
| [Population by Ethnicity and Region (2021)](https://www.data.gov.uk) | 2021 Census | Ethnicity, Geography, Ethnic Population, % shares |
| [Prosecutions and Convictions](https://www.data.gov.uk) | 2009–2017 | Ethnicity, Age group, Sex, Offence group, Police Force Area, Prosecution and conviction counts |
| [Stop and Search 2006–2023](https://www.data.gov.uk) | 2006–2023 | Ethnicity, Geography, Year, S&S counts, Rate per 1,000, Proportion by ethnicity |


---

## Repository Structure

```
├── Data/
│   ├── population-by-ethnicity-and-region-2021.csv
│   ├── prosecutions-and-convictions.csv
│   ├── stop-and-search-2006-2023.csv
├── Code_and_Report.ipynb
└── README.md
```

---

## How to Run

### Requirements
- Python 3.13.5
- Jupyter Notebook

### Install dependencies

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

Or save the following as `requirements.txt` and run `pip install -r requirements.txt`:

```
pandas
numpy
matplotlib
seaborn
jupyter
```

### Run the notebook

```bash
jupyter notebook Code_and_Report.ipynb
```

> Make sure all three CSV files are placed inside the `Data/` folder with the exact filenames referenced in the notebook before running.

---

## Methodology

1. Datasets were imported using `pd.read_csv` with `latin-1` encoding to handle special characters common in government data exports.
2. Copies of original dataframes were preserved throughout analysis to allow rollback if needed.
3. Data exploration was performed using `.info()` and iterative loops to inspect null value counts and unique value distributions per column.
4. Missing data was handled as follows:
   - Columns with more than 50% null values were dropped using `.dropna(thresh=len(df)/2)`.
   - Rows where the prosecution denominator was null were dropped from df2 entirely, as they cannot contribute to ratio-based analysis.
   - Numerical columns in df3 (stop and search counts, rates, proportions) had nulls filled with 0.
   - The `population_by_ethnicity` column was imputed using the column median.
5. A **conviction rate** derived metric was computed as `Convictions / Prosecutions × 100` and used throughout the analysis.
6. Ethnicity labels in df3 were harmonised to the five-category ONS broad classification (White, Black, Asian, Mixed, Other inc. Chinese) to enable cross-dataset merging with df2.
7. Financial year labels in df3 (e.g. `2009/10`) were converted to integer years using the first year of each period.
8. Inter-dataset merges were performed on shared keys (geography, ethnicity, time) to draw cross-dataset inferences.
9. All visualisations were produced using `matplotlib` and `seaborn`, with colour palettes chosen for accessibility and clarity.

---

## Analysis and Findings

### 1. Ethnic Population Distribution

White groups constitute **81.7%** of the total population of England and Wales in 2021. Asian is the second largest group at 9.3%, followed by Black (4.0%), Mixed (2.9%), and Other (2.1%).

This demographic baseline is the essential context for all downstream analysis. A group comprising 81.7% of the population dominating absolute prosecution counts is expected — disproportionality only becomes visible when counts are normalised by population size.

Regional variation is significant: London has by far the highest non-White population share, while the North East and Wales have the lowest ethnic diversity. Regional prosecution and stop and search patterns cannot be fairly compared without accounting for this.

---

### 2. Prosecutions and Convictions Over Time

Total prosecutions fell consistently from 2009 to 2017 across all ethnicities. However, the **conviction rate rose** over the same period — from approximately 76% in 2009 to 83% by 2017.

This combination — fewer prosecutions but a higher proportion resulting in conviction — indicates that prosecutorial decision-making became more selective over time. Cases are less frequently brought to court, but those that are brought increasingly result in a guilty verdict, consistent with CPS charging standard reforms introduced during this period.

---

### 3. Conviction Rate by Ethnicity

When conviction rates are disaggregated by ethnicity, a persistent gap emerges:

- **White** and **Other inc. Chinese** groups have the highest conviction rates (~83–85%)
- **Asian** and **Mixed** groups have the lowest (~75–79%)
- **Black** groups sit in the middle (~78%)

This gap is present across the full 2009–2017 period and is not explained simply by offence type. It may reflect differences in case strength at the point of charge, quality of legal representation, or other systemic factors that affect court outcomes by ethnicity.

---

### 4. Gender Gap in Prosecutions

Males account for **6.2 times** more prosecutions than females across all ethnicities combined. This gender gap is larger than any ethnic gap in the data and holds consistently across all ethnic groups.

The data also reveals that female prosecution rates are notably higher for Black women relative to other female ethnic groups — a dimension that merits further investigation but is underexplored in existing government reporting on this dataset.

---

### 5. Conviction Rate by Offence Group

Conviction rates vary substantially by offence type:

| Offence Group | Conviction Rate |
|---|---|
| Public order offences | ~92% |
| Drug offences | ~90% |
| Theft offences | ~85% |
| Fraud offences | ~83% |
| Possession of weapons | ~74% |
| Criminal damage and arson | ~72% |
| Miscellaneous crimes against society | ~72% |
| Robbery | ~62% |
| Violence against the person | ~62% |
| Sexual offences | ~52% |

The very high conviction rate for drug offences (90%) is significant when read alongside the stop and search data. Drug searches are common, and when they result in prosecution they almost always result in conviction — making drug-motivated stop and searches among the most consequential for individuals stopped.

Sexual offences at ~52% reflect the well-documented evidential challenges in these cases, typically relying on witness testimony without independent corroboration.

---

### 6. Prosecutions by Age Group

Prosecution rates increase progressively from juveniles to young adults to adults across all ethnic groups. The jump from juveniles to young adults is steep, partly reflecting youth diversion schemes that route younger offenders away from formal prosecution.

The relatively higher juvenile proportion for Black individuals compared to other groups may reflect differential enforcement at younger ages or socioeconomic factors that increase early contact with the justice system — both of which warrant further investigation alongside social deprivation data.

---

### 7. Prosecutions by Offence Group and Ethnicity

White, Asian, and Black groups saw their highest prosecution counts in **drug offences**. Mixed and Other inc. Chinese groups saw the highest counts in **theft offences**.

The prominence of drug offences for Asian and Black groups — despite their smaller population share — is notable when combined with the stop and search data. Stop and searches are frequently motivated by drug suspicion, drug prosecutions have a ~90% conviction rate, and Black and Asian groups are stopped at disproportionate rates. This creates a compounding dynamic where enforcement decisions at the stop and search stage shape which offence types different ethnic groups are ultimately prosecuted for.

---

### 8. Stop and Search — National Trend (2006–2023)

Total stop and searches peaked at over **4 million** in 2009 and fell sharply to under 900,000 by 2017 following the government's *Best Use of Stop and Search* scheme in 2014. A secondary rise began from 2018, associated with county lines drug enforcement and knife crime initiatives.

Crucially, crime rates did not spike during the 2014–2017 period of reduced stop and search — challenging the assumption that high S&S volumes are necessary for public safety.

---

### 9. Stop and Search Disproportionality — Black vs. White

Black individuals are stopped at a rate consistently **4 to 9.5 times higher** than White individuals per 1,000 population across the 2006–2023 period.

The disproportionality ratio peaked at **9.6x** in 2017 — after the reduction policy had been in force for three years. The S&S reduction disproportionately benefited White individuals: as total volumes fell, the remaining stops became more concentrated on Black individuals. This indicates the reforms did not address the structural causes of disproportionality.

---

### 10. Stop and Search Efficiency — Stops per Prosecution

When stop and search volumes are compared against prosecution counts across the overlapping 2009–2017 period, a clear pattern emerges:

- **White individuals** require the most stop and searches per prosecution — S&S of White individuals is the least efficient at generating prosecutions.
- **Black individuals** require the fewest stop and searches per prosecution — each stop is most likely to result in prosecution.

This finding is paradoxical. Despite being stopped at up to 9.5x the rate of White individuals, stops of Black individuals more frequently result in prosecution. This could indicate more targeted (intelligence-led) stopping of Black individuals, or differential prosecution thresholds by ethnicity, or both. Neither interpretation is straightforward, and both demand further scrutiny.

---

### 11. Cross-Dataset: Conviction Rate by Ethnicity and Offence Group

A heatmap of conviction rates across all ethnicity–offence combinations reveals that:

- The ethnicity gap in conviction rates is largest for **violent offences** and **robbery**, where case quality differences, witness cooperation rates, or jury composition effects may operate differently across ethnic groups.
- Drug and public order offence conviction rates are consistently high and relatively uniform across ethnicities — once charged, these cases succeed regardless of the defendant's ethnic background.
- Sexual offence conviction rates are the lowest across the board, with Asian individuals showing the lowest rates in this category (~47%).

---

### 12. Police Force Area Comparison

The Metropolitan Police Area leads by a substantial margin in both total prosecutions and total stop and searches. Greater Manchester is second in prosecutions but its S&S volume relative to prosecution count is notably lower — suggesting a more efficient conversion of stops into prosecutions compared to the Metropolitan area.

In the Metropolitan area, the ratio of White to non-White prosecutions is closer than in other regions, consistent with London's significantly more diverse population.

---

## Conclusions

1. **Demographic baseline is essential.** White groups make up 81.7% of England and Wales. Absolute prosecution and S&S counts must always be read against population proportions — raw counts alone are misleading.

2. **Prosecutions are falling; conviction rates are rising.** Fewer cases are being brought to court, but those that are brought succeed more often. This points to more selective, evidence-based charging decisions over time.

3. **A persistent conviction rate gap exists by ethnicity.** White and Other inc. Chinese individuals have the highest conviction rates. Asian and Mixed individuals have the lowest. This gap persists across time and is not fully explained by offence type differences.

4. **The gender gap in prosecutions is larger than any ethnic gap.** Males account for 6.2x more prosecutions than females — a consistent finding that receives comparatively little policy attention.

5. **Drug and public order offences have ~90% conviction rates.** Once charged for these offences, conviction is near-certain regardless of ethnicity.

6. **Black individuals are stopped at 4–9.5x the rate of White individuals.** This disproportionality worsened after 2014 even as total S&S volumes fell — meaning reform benefited White individuals more than Black individuals.

7. **S&S of Black individuals is the most efficient at generating prosecutions.** Despite the highest stop rate, Black individuals also have the lowest number of stops required per prosecution. Whether this reflects more targeted policing or differential prosecution thresholds remains an open question.

8. **Metropolitan Police and Greater Manchester** dominate in both prosecution volumes and stop and search activity across the study period.

---

## Limitations

- Population data is from 2021 only and cannot serve as a time-varying denominator for the 2006–2023 stop and search data, meaning rate calculations for earlier years carry demographic uncertainty.
- The prosecutions dataset covers only 2009–2017, preventing direct comparison with the full S&S timeline and any post-2017 trends.
- Geographic name mismatches between datasets (e.g. `Avon & Somerset` vs `Avon and Somerset`) limited the scope of police force area cross-analysis and required manual reconciliation.
- Many-to-many merges on ethnicity across datasets produced duplicate rows requiring careful deduplication, which may have affected some aggregated values.
- All ethnicity findings involving absolute counts are confounded by population size differences. Rate-based normalisation was applied where population data allowed but was not possible across all dimensions.
- The dataset is dominated by White ethnicity in absolute terms. Confidence intervals on findings for smaller ethnic groups (e.g. Other inc. Chinese) are implicitly wider due to lower base counts.

---

## Recommendations

1. **Normalise all prosecution and conviction figures by population size** (rate per 100,000) to enable fair cross-ethnic and cross-regional comparison. The raw datasets do not include this — it must be derived.

2. **Extend the prosecutions dataset beyond 2017** to align with the stop and search data and capture post-county-lines and post-COVID trends.

3. **Include deprivation index and socioeconomic data as control variables** before drawing causal conclusions about ethnicity and criminal justice outcomes. Much of the observed disproportionality may be partially mediated by socioeconomic deprivation, which correlates with both ethnicity and criminal justice contact.

4. **Standardise geographic naming conventions across data.gov.uk datasets** to facilitate automated merging without manual reconciliation.

5. **Disaggregate by both sex and ethnicity simultaneously** in future analyses — the interaction between these two dimensions is currently underexplored both in this project and in the published government statistics.

6. **Use time-varying population estimates** (annual mid-year population estimates by ethnicity) rather than the 2021 Census snapshot to improve rate calculations across the full 2006–2023 stop and search period.

---

## Libraries Used

| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, merging, and aggregation |
| `numpy` | Numerical operations and array handling |
| `matplotlib` | Primary visualisation (bar charts, line charts, scatter plots, area charts) |
| `seaborn` | Styling, colour palettes, heatmaps |

---

## References

- learnpython.org — https://www.learnpython.org/
- GeeksforGeeks — Chart Type Selection Guide — https://www.geeksforgeeks.org/data-visualization/choosing-the-right-chart-type-a-technical-guide/
- data.gov.uk — Population by Ethnicity and Region 2021 — https://www.data.gov.uk
- data.gov.uk — Prosecutions and Convictions — https://www.data.gov.uk
- data.gov.uk — Stop and Search 2006–2023 — https://www.data.gov.uk

---

