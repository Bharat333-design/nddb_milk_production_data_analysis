# nddb_milk_production_data_analysis
The milk production data was extracted from NDDB website for period 2001-24. The data is original. An investigation, descriptive analysis is done along with states and regional performance and ranking states based on their production. And created an excel dashboard for displaying the found insights.

## Introduction
India is the biggest producer and consumer of milk and milk products in the world. The demand for milk often concedes the supply of the milk. Historically, India has been an agrarian economy. India did a lot of investment in dairy sector encouraging dairy farming in each state to boost domestic milk production.
This project aims at finding how much progress India made in milk sector for the period 2001-24. Finding the trends region and state wise. Finding the top performing states and regions along with least performing states. Finding the Golden Points where milk production took off. 
- The raw dataset contains year, milk production in that year and the state. The dataset file in pdf format. 
- The dataset is downloaded from NDDB official website.
- Data is recorded for the period 2001-24.

## Data Gathering 
Data was extracted from PDF available on [National Dairy Development Board (NDDB)](https://www.nddb.coop/information/stats/milkprodstate). Using Copilot, extracted and restructured data from pdf into excel file.

New Structure :

| Year | State | Milk |
|------|-------|------|
|2001-02| Goa | 546 |

## Data Cleaning and Feature Engineering
- Added a new column by name "Region". Assigned values in Region column based on the States Location.
  Regions :
    - Central India
    - North India
    - South India
    - East India
    - West India
    - North East India
- Checked for null values using the data filter button. Found null values in values inor the Milk Column where data for some   states is not recorded. Filled the null values based on the median of last two and next two yearly milk production to bring consistency.
    - For example:
       
| Year | State | Milk |
|------|-------|------|
|2001-02| Goa |  120 |
|2002-03| Goa | null |
|2003-04| Goa | 160 |
|2004-05| Goa | 170 |
|2005-06| Goa | 230 |

Median(0,120,160,170) → __140__ (Fill Value) 

__Formula Used:__ 

```Excel
IF(ISBLANK(E2),
   MEDIAN(
      IFERROR(INDEX(E:E,ROW()-2),NA()),
      IFERROR(INDEX(E:E,ROW()-1),NA()),
      IFERROR(INDEX(E:E,ROW()+1),NA()),
      IFERROR(INDEX(E:E,ROW()+2),NA())
    ),
   E2)
```

- Checking uniqueness of Region and State Names
  Checked if the State and Region names are standard or not using the data filter button. Found __North East India__ and __North Eastern India__ non-standard values representing same region.

    - Replaced the __North Eastern India__ with __North East India__ using __Find & Replace__.
    - Re-checked the Region names uniqueness. Found all value unique.

- Checking If All Yearly Records Are Available For Each State
  Selected each state individually using the data filter button and filtered data for each state. Found all years and milk     production data available for state.

> [!Note]
> The Data is cleaned ready for analysis.

## Data Analysis
Using pivot table found the following insights.
- State's total production during the period or at any given point of time using year filter.
- Region wise milk production
- State's total production region wise with Region as filter
- Yearly milk production with States and Region as filter
- 
