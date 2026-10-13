# nddb_milk_production_data_analysis
The milk production data was extracted from NDDB website for period 2001-24. The data is original. An investigation, descriptive analysis is done along with states and regional performance and ranking states based on their production. And created an excel dashboard for displaying the found insights.

## Introduction
India is the biggest producer and consumer of milk and milk products in the world. The demand for milk often concedes the supply of the milk. Historically, India has been an agrarian economy. India did a lot of investment in dairy sector encouraging dairy farming in each state to boost domestic milk production.
This project aims at finding how much progress India made in milk sector for the period 2001-24. Finding the trends region and state wise. Finding the top performing states and regions along with least performing states. Finding the Golden Points where milk production took off. 
- The raw dataset contains year, milk production in that year and the state. The dataset file in pdf format. 
- The dataset is downloaded from NDDB official website.
- Data is recorded for the period 2001-24.

## Data Gathering 
Data was extracted from PDF available on [National Dairy Development Board (NDDB)](https://www.nddb.coop/information/stats/milkprodstate). Using Copilot, extracted and restructured data from pdf and saved in an excel file to speed up the process.

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

Put Milk in Value and Region, State and Year in Filter and Rows based on query.

Found the total growth in milk production using simple division. Used following formula to find total growth:
```Excel
= ROUND( (X2- B2)/B2,2)
```
Where `X2` represents milk production in the max year which is 2023-24 and `B2` the milk production in the min year that is 2001-02.

Calculated dynamic total milk production using `Pivot Table`
- Used Milk in value
- Used Year and State in filter

Golden Cross and Moving Averages

## Insights

- National production nearly doubled from 2001 to 2024 with about 1.84 times increase from 87062 metric tonne to 195266 metric tonne.
- Bihar recorded the highest growth with about 3.8 times increased milk production from 2001 to 2024. Followed by Rajasthan and MP with about 3.5 times and 3 times respectively.
- Following states beat the national growth
    - Bihar __(384% growth)__
    - Rajasthan __(350% growth)__
    - MP __(300% growth)__
    - Jharkhand __(220% growth)__
    - Gujrat __(210% growth)__
    - Ladakh __(210% growth)__
    - Lakshadweep __(200% growth)__

<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/40c21945-a775-4cd2-8caf-63c8be13b342" />

 
- States Ranking
  | Rank | 2001 | 2024 |
  |------|------|------|
  |1| Uttar Pradesh | Uttar Pradesh
  |2| Punjab| Madhya Pradesh
  |3| Maharashtra| Gujrat
  |4| Gujrat| Maharashtra
  |5| Andhra Pradesh| Andhra Pradesh
  |6| Madhya Pradesh| Karnatka
  |7| Haryana| Bihar
  |8| Tamil Nadu| Haryana
  |9| West Bengal| Telangna
  |10| Karnatka| Punjab

  > [!Note]
  > • Uttar Pradesh maintains top position despite lower growth than national growth which explains the scale of milk production in UP.
  > • Punjab has fallen through the ranks from second to tenth rank. It is one of the least states with least growth of about 77% in 24 years above only to North East States and UTs.
  > • Tripura only North Eastern State with high growth of about 180%.

  Contribution
  - North and South Region together contributes to 61% of national production.
      - North India (36%)
      - South India (25%)
      - West India (16%)
      - East India (13%)
      - Central India (9%)
      - North East India (1%)

  <img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/5148cf43-21e4-4420-883b-860c77e35b9d" />


  - Top 5 States contributes to 48% of national production.
      - Uttar Pradesh (13%)
      - Madhya Pradesh (11%)
      - Gujrat (9%)
      - Maharashtra (8%)
      - Andhra Pradesh (7%)

<img width="250" height="200" alt="image" src="https://github.com/user-attachments/assets/1ec0bf5c-8a5f-4a02-825b-67eabd04e2b0" />
<img width="250" height="200" alt="image" src="https://github.com/user-attachments/assets/56926697-9307-4d2d-93e9-850bcf5a2d3d" />



  - Golden Dip and Golden Cross
    When yearly growth % crosses the 5 year rolling percentage, it is called golden cross describing a trend breaker. Same is the case for Golden Dip when reverse happens.

    The chart below displays the Golden Dip and Golden Cross.
      - First 5 years from 2001- 2005 can be ignored due to lack of past years data.
      - The trend considered and observed post 2005.

    Golden Dip 1
      - The golden dip happens in 2012-13 when the yearly growth % crosses down 5 year rolling average.
      - The fall continues to 2014-15. The Situation worsens in 2014-15 with an annual growth rate of just 1.34%.
      - The fall is due to an inexplicable event.
    
    Golden Cross
      - The golden cross happens in 2015-16 when yearly growth cross the 5 year rolling average.
      - The rise continues till 2019-20.
    
    Golden Dip 2
      - The golden dip happens in 2019-20 and continues the down trend till the latest recorded year that is 2024.
      - The primary reason of this down trend can be covid-19 and its after effects.
      - The yearly growth still moved around average yearly growth which is 3.58% but takes a sudden in explicable dip in 2024.
    Golden Period
      - From 2015 to 2021 the yearly growth rate moves from 4% to more than 5% beating the 5 year rolling average and overall average growth by considerable margins.
  
  <img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/7b28abb8-9210-4886-b8e0-1ec2a8acae31" />

| Year    | Growth (%) |
|---------|------------|
| 2001-02 | 0.00%      |
| 2002-03 | 2.85%      |
| 2003-04 | 1.95%      |
| 2004-05 | 4.95%      |
| 2005-06 | 3.54%      |
| 2006-07 | 3.32%      |
| 2007-08 | 4.02%      |
| 2008-09 | 3.66%      |
| 2009-10 | 3.65%      |
| 2010-11 | 4.05%      |
| 2011-12 | 4.16%      |
| 2012-13 | 3.45%      |
| 2013-14 | 3.52%      |
| 2014-15 | 1.34%      |
| 2015-16 | 4.97%      |
| 2016-17 | 4.38%      |
| 2017-18 | 5.42%      |
| 2018-19 | 5.22%      |
| 2019-20 | 4.29%      |
| 2020-21 | 3.88%      |
| 2021-22 | 3.90%      |
| 2022-23 | 3.15%      |


  

