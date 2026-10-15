
# India Milk Production Analysis (2001–2024)

An exploratory and descriptive analysis of India's state-wise milk production from 2001–02 to 2023–24, using data published by the **National Dairy Development Board (NDDB)**. This project examines national, regional, and state-level trends, compares state rankings, identifies periods of faster and slower growth, and presents the findings in an Excel dashboard.

## Table of Contents

- [Introduction](#introduction)
- [Dataset Overview](#dataset-overview)
- [Data Gathering](#data-gathering)
- [Data Cleaning and Feature Engineering](#data-cleaning-and-feature-engineering)
- [Analysis Approach](#analysis-approach)
- [Key Insights](#key-insights)
- [State Rankings](#state-rankings)
- [Regional Contribution](#regional-contribution)
- [Golden Dip and Golden Cross](#golden-dip-golden-cross-and-growth-periods)
- [State-Level Observations](#state-level-observations)
- [Regional Trends](#regional-trends)
- [Regional Leaders](#regional-leaders)
- [India-Level Concentration](#india-level-concentration)
- [Dashboard](#dashboard)

## Introduction

India is the world's largest producer and consumer of milk and milk products. Demand for milk can at times outpace supply. Historically, India has been an agrarian economy, and investment in the dairy sector has encouraged dairy farming across states to increase domestic milk production.

This project investigates how India's milk sector progressed over the period **2001–02 to 2023–24**. It explores:

- National milk-production trends over time.
- State-wise and region-wise performance.
- The highest- and lowest-performing states and regions.
- Changes in state rankings.
- Significant periods when milk-production growth accelerated or slowed.

## Dataset Overview

- **Source:** [National Dairy Development Board (NDDB)](https://www.nddb.coop/information/stats/milkprodstate)
- **Period covered:** 2001–02 to 2023–24
- **Original format:** PDF
- **Number of rows:** 689
- **Core fields:** Year, State, and Milk production

The dataset contains annual milk-production records for Indian states and union territories, as available in the source.

## Data Gathering

The data was extracted from the PDF published on the [NDDB website](https://www.nddb.coop/information/stats/milkprodstate). Microsoft Copilot was used to speed up extraction and restructuring of the PDF data into an Excel file.

The data was reorganized into the following structure:

| Year | State | Milk |
|---|---|---:|
| 2001–02 | Goa | 546 |

## Data Cleaning and Feature Engineering

### 1. Created a Region Column

A new column named `Region` was added. Each state was assigned to a region based on its location.

The regions used in the analysis were:

- Central India
- North India
- South India
- East India
- West India
- North East India

### 2. Handled Missing Milk-Production Values

Null values were checked using Excel's filter feature. Missing values were found in the `Milk` column for some state-year records where data was not recorded.

To maintain consistency, missing values were filled using the **median of the two preceding and two following yearly milk-production values**, where available.

Example:

| Year | State | Milk |
|---|---|---:|
| 2001–02 | Goa | 120 |
| 2002–03 | Goa | *null* |
| 2003–04 | Goa | 160 |
| 2004–05 | Goa | 170 |
| 2005–06 | Goa | 230 |

The example calculation used in the original analysis was:

`Median(0, 120, 160, 170) → 140`

**Excel formula used:**

```excel
=IF(ISBLANK(E2),
   MEDIAN(
      IFERROR(INDEX(E:E,ROW()-2),NA()),
      IFERROR(INDEX(E:E,ROW()-1),NA()),
      IFERROR(INDEX(E:E,ROW()+1),NA()),
      IFERROR(INDEX(E:E,ROW()+2),NA())
   ),
   E2
)
```

### 3. Standardized Region Names

The region and state names were checked for consistency using Excel's filter feature.

Two labels, `North East India` and `North Eastern India`, were found to refer to the same region.

- Replaced `North Eastern India` with `North East India` using **Find & Replace**.
- Rechecked the region names to confirm consistency.

### 4. Checked Yearly Coverage by State

Each state was filtered individually to check whether its yearly records were available. The review indicated that all years and milk-production records were available for each state after the cleaning process.

> **Data-cleaning status:** The dataset was considered ready for analysis after these checks.

## Analysis Approach

Pivot tables were used to explore the dataset and calculate:

- Total milk production by state over the full period, or for a selected year using the year filter.
- Region-wise milk production.
- State-wise production within a selected region.
- Yearly milk production with state and region filters.

Depending on the question, `Milk` was placed in **Values**, while `Region`, `State`, and `Year` were used in **Rows** and/or **Filters**.

### Total Growth in Milk Production

Total growth was calculated using the following Excel formula:

```excel
=ROUND((X2-B2)/B2,2)
```

Where:

- `X2` represents milk production in the latest year, **2023–24**.
- `B2` represents milk production in the earliest year, **2001–02**.

### Dynamic Total Milk Production

A pivot table was used to calculate dynamic total milk production:

- **Values:** `Milk`
- **Filters:** `Year` and `State`

### Yearly Growth and Five-Year Rolling Average

The yearly growth series and five-year rolling average were used to identify periods when annual growth moved above or below the rolling average.

Steps followed:

1. Created a yearly milk-production table using a pivot table, with `Year` in Rows and `Milk` in Values.
2. Right-clicked the pivot table and selected **Show Values As → % Difference From**.
3. Set the base field to `Year` and the base item to `(previous)`.
4. Copied the year and yearly-growth columns using **Paste Special → Values**.
5. Added a column for the five-year rolling average.
6. Calculated the rolling average using:

```excel
=AVERAGE(OFFSET(N4,-4,0,5,1))
```

7. Inserted a line chart using the year, yearly growth, and five-year rolling-average series.

## Key Insights

### National and State Growth

- National milk production increased by approximately **1.84 times** from 2001 to 2024, rising from **87,062 metric tonnes** to **195,266 metric tonnes**, according to the project's calculations.
- Bihar recorded the highest growth, with milk production increasing by approximately **3.8 times** from 2001 to 2024.
- Rajasthan and Madhya Pradesh followed, with increases of approximately **3.5 times** and **3 times**, respectively.

The following states and union territories were reported to have outpaced national growth:

| State / Union Territory | Reported Growth |
|---|---:|
| Bihar | 384% |
| Rajasthan | 350% |
| Madhya Pradesh | 300% |
| Jharkhand | 220% |
| Gujarat | 210% |
| Ladakh | 210% |
| Lakshadweep | 200% |

![State-wise milk-production growth chart](https://github.com/user-attachments/assets/40c21945-a775-4cd2-8caf-63c8be13b342)

### State Rankings

The table compares the highest-producing states in 2001 and 2024, as recorded in the analysis.

| Rank | 2001 | 2024 |
|---:|---|---|
| 1 | Uttar Pradesh | Uttar Pradesh |
| 2 | Punjab | Madhya Pradesh |
| 3 | Maharashtra | Gujarat |
| 4 | Gujarat | Maharashtra |
| 5 | Andhra Pradesh | Andhra Pradesh |
| 6 | Madhya Pradesh | Karnataka |
| 7 | Haryana | Bihar |
| 8 | Tamil Nadu | Haryana |
| 9 | West Bengal | Telangana |
| 10 | Karnataka | Punjab |

**Observations:**

- **Uttar Pradesh** maintained the top position despite growing more slowly than the national rate, highlighting the scale of its milk production.
- **Punjab** fell from second to tenth place. The project reports growth of about 77% over 24 years, among the lowest rates apart from North-Eastern states and union territories.
- **Tripura** was identified as the only North-Eastern state with high growth, at approximately 180%.

### Regional Contribution

The project reports that North and South India together contribute a substantial share of national milk production.

| Region | Reported Contribution |
|---|---:|
| North India | 36% |
| South India | 25% |
| West India | 16% |
| East India | 13% |
| Central India | 9% |
| North East India | 1% |

North and South India together account for **61%** of national production according to this analysis.

![Regional contribution chart](https://github.com/user-attachments/assets/5148cf43-21e4-4420-883b-860c77e35b9d)

### Contribution of the Top Five States

The project's analysis reports that the top five states contribute **48%** of national milk production.

| State | Reported Contribution |
|---|---:|
| Uttar Pradesh | 13% |
| Madhya Pradesh | 11% |
| Gujarat | 9% |
| Maharashtra | 8% |
| Andhra Pradesh | 7% |

![Top states contribution chart 1](https://github.com/user-attachments/assets/1ec0bf5c-8a5f-4a02-825b-67eabd04e2b0)

![Top states contribution chart 2](https://github.com/user-attachments/assets/56926697-9307-4d2d-93e9-850bcf5a2d3d)

### Golden Dip, Golden Cross, and Growth Periods

In this project, a **Golden Cross** refers to annual growth crossing above the five-year rolling average, while a **Golden Dip** refers to annual growth crossing below the five-year rolling average. These labels describe changes in the milk-production growth trend.

The first five years (2001–02 to 2005–06) can be treated cautiously because fewer preceding years are available for a five-year rolling comparison. The analysis focuses on the period after 2005.

#### Golden Dip 1: 2012–13 Onward

- The first Golden Dip occurred in **2012–13**, when annual growth crossed below the five-year rolling average.
- The decline continued through **2014–15**.
- In 2014–15, the annual growth rate fell to just **1.34%**.
- The project notes that the cause of this decline was not identified.

#### Golden Cross: 2015–16 Onward

- The Golden Cross occurred in **2015–16**, when annual growth crossed above the five-year rolling average.
- The upward trend continued until **2019–20**.

#### Golden Dip 2: 2019–20 Onward

- The second Golden Dip was identified in **2019–20**, followed by a downward trend through the latest recorded year, 2023–24.
- The project proposes COVID-19 and its after-effects as a possible explanation for this trend.
- Annual growth continued to fluctuate around the reported average annual growth rate of **3.58%**, but the analysis notes a sudden, unexplained dip in 2024.

#### Golden Period: 2015–16 to 2020–21

- From 2015–16 through 2020–21, annual growth generally ranged from around **4% to more than 5%**, exceeding the five-year rolling average and the reported overall average by considerable margins.

![Yearly growth and five-year rolling average chart](https://github.com/user-attachments/assets/7b28abb8-9210-4886-b8e0-1ec2a8acae31)

#### Annual Growth Table

| Year | Growth (%) |
|---|---:|
| 2001–02 | 0.00% |
| 2002–03 | 2.85% |
| 2003–04 | 1.95% |
| 2004–05 | 4.95% |
| 2005–06 | 3.54% |
| 2006–07 | 3.32% |
| 2007–08 | 4.02% |
| 2008–09 | 3.66% |
| 2009–10 | 3.65% |
| 2010–11 | 4.05% |
| 2011–12 | 4.16% |
| 2012–13 | 3.45% |
| 2013–14 | 3.52% |
| 2014–15 | 1.34% |
| 2015–16 | 4.97% |
| 2016–17 | 4.38% |
| 2017–18 | 5.42% |
| 2018–19 | 5.22% |
| 2019–20 | 4.29% |
| 2020–21 | 3.88% |
| 2021–22 | 3.90% |
| 2022–23 | 3.15% |

*The growth table ends at 2022–23, while other sections describe trends through 2023–24.*

### State-Level Observations

| State | Observation |
|---|---|
| Uttar Pradesh | Consistent No. 1 since 2001. |
| Madhya Pradesh | Emerged strongly over the last 10 years; consistently in the top three, with high production volumes. |
| Gujarat | A major milk producer; consistently in the top four since 2001. |
| Maharashtra | Consistent performer; maintained fourth or fifth position throughout. |
| Andhra Pradesh | Historically a high producer; dropped in rank as Madhya Pradesh, Gujarat, and Maharashtra rose. |
| Punjab | Consistently declining in rank, despite continued growth. |
| Bihar and Rajasthan | Strong growth, but lower production volumes than the top states. |
| Haryana | Linear growth after 2020 (COVID); the project anticipates a possible boom after 2024–25. |

### Regional Trends

- **Central India:** Strong growth after 2012.
- **North East India:** Stable growth, with no extraordinary change identified.
- **West India:** Consistent growth since 2008.
- **South India:** Consistent growth throughout the period.

### Regional Leaders

The project identifies the following states as the main contributors within their respective regions:

- **Central India:** Madhya Pradesh alone produces **90%** of the region's milk.
- **East India:** Bihar (**48%**) and West Bengal (**31%**) together account for **79%** of the region's milk.
- **North East India:** Assam (**67%**) and Tripura (**16%**) dominate regional production.
- **North India:** Uttar Pradesh (**50%**), Haryana (**20%**), and Punjab (**14%**) together account for **77%**; Rajasthan adds another **11.5%**.
- **South India:** Andhra Pradesh (**29%**), Karnataka (**28%**), and Telangana (**21%**) together account for **78%**.
- **West India:** Gujarat (**53%**) and Maharashtra (**46%**) together account for **99%**.

### India-Level Concentration

The project highlights the concentration of milk production across a small number of states and regions:

- **Big Fish 1 — States:** Uttar Pradesh (**13%**), Madhya Pradesh (**10%**), Gujarat (**9%**), Maharashtra (**8%**), and Andhra Pradesh (**7%**) together account for **48.8%** of India's milk production.
- **Big Fish 2 — Regions:** North India (**31.3%**) and South India (**24%**) together account for **55.3%** of India's milk production.
- **Big Fish 3 — Regional distribution:**
  - North India: 31%
  - South India: 24%
  - West India: 17%
  - Central India: 12%
  - East India: 14%
  - North East India: 0.01%

## Dashboard

*Dashboard details and screenshots to be added.*

[![Watch the demo](assets/dashboard-thumbnail.png)](https://github.com/yourusername/yourrepo/assets/dashboard-video-milk.mp4)

## Notes for Validation

Before publishing the project, consider checking the following items against the source data and Excel workbook:

1. **Missing-value example:** The example shows `Median(0, 120, 160, 170) → 140`. Confirm which four values are included and whether `0` represents a missing or actual value.
2. **Units:** Confirm the unit used for milk-production values. Verify whether the NDDB source uses tonnes, thousand tonnes, lakh tonnes, or another unit before presenting the national totals.
3. **Growth figures and years:** Verify that national and state growth calculations compare the same start and end years, and that the reported times-increase and percentage-growth figures are consistent.
4. **Regional contribution totals:** Regional contribution figures differ between sections. For example, North India is listed as 36% in one section and 31–31.3% in another. Confirm the year or calculation basis used for each table.
5. **North-East India share:** The value `0.01%` in the India-level distribution differs from the `1%` reported in the regional contribution table. Check for a possible typo or a different calculation basis.
6. **2023–24 growth:** The annual growth table stops at 2022–23, although the trend discussion extends to 2023–24. Add the 2023–24 growth value if it is available.
7. **COVID-19 explanation and future outlook:** COVID-19 effects and the expected post-2024–25 growth in Haryana are interpretations or hypotheses, not demonstrated causal findings. Consider validating these claims with supporting evidence.
8. **Golden Cross / Golden Dip terminology:** These labels describe annual growth crossing a five-year rolling average in this project. Define them as project-specific labels to avoid confusion with other common uses of the terms.

---

**Data Source:** [National Dairy Development Board (NDDB) — State-wise Milk Production](https://www.nddb.coop/information/stats/milkprodstate)
