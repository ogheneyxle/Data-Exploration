# Data-Exploration

## Table of Content
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Preparation](#data-preparation)
- [Results](#results)
- [Recommendations](#recommendations)
- [Limitations](#limitations)

### Project Overview
In this project, I decided to take a closer look at the layoffs data, querying the entries, identifying trends that may inform future actions. 

### Data Sources
Layoffs Data: The primary data source for this data is the “layoffs.csv” file, containing detailed information regarding how many layoffs a company made per year, per location.

### Tools
- SQL

### Data Preparation
With this dataset, there a ton of questions we can ask. With the percentage_laid_off and total_laid_off columns as a basis, below are the ones we focused on in this project;
- What companies let go of their total workforce?
- How many people were let go per company?
- How much money was raised by these companies?
- Within what time period were these people laid off?
- What country had the most layoffs?
- What year had the most layoffs?
- What company let go of the most staff?

### Data Analysis
- In order to ascertain which companies laid off 100% of their workforce i.e, went under, we use the following command;
```SQL
select *
from layoffs_staging2
where percentage_laid_off = 1;
```
- In the event that these companies shut down because they couldn't raise enough funds, we can determine if this is the case with the following command;
```SQL
select *
from layoffs_staging2
where percentage_laid_off = 1
order by funds_raised_millions desc;
```
- We can also inspect the time period these layoffs occurred, to do know this, we used the following command;
```SQL
select min(`date`), max(`date`)
from layoffs_staging2;
```
- We can do deeper and query which industries, countries and year had the most layoffs with the following commands;
Industry query
```SQL
select industry, sum(total_laid_off)
from layoffs_staging2
group by industry
order by 2 desc;
```
Country query
```SQL
select country, sum(total_laid_off)
from layoffs_staging2
group by country
order by 2 desc;
```
Year query
```SQL
select year(`date`), sum(total_laid_off)
from layoffs_staging2
group by year(`date`)
order by 1 desc;
```
- Finally we can check what industry had the most layoffs across the time period of 2020 to 2023;
```SQL
select industry, sum(total_laid_off)
from layoffs_staging2
group by industry
order by 2 desc;
```

There are more queries you can execute in your own analysis, depending on what results you want for your own data analysis. 

### Results
The findings from this data exploration project are as follows;
1. 2023 has the highest amount of layoffs with 125677 in total.
2. Google, Meta, Amazon, and Microsoft accounts for a large number of the layoffs with 43000 in 2023 alone.
3. Uber has the most layoffs overall
4. The industries with the most layoffs are Consumer, Retail, and Other.

### Recommendations
Based on the results from our exploration of the layoffs data, I recommend the following;
1. Invest in the AirBnB sector, it showed great returns and didnt have as much layoffs

### Limitations
With data sourced from around the globe, from different companies in different countries at different stages, it is not uncommon for the reported data to only closely resemble the true story. Thus number of layoffs recorded does not accurately represent the extent to which the covid pandemic truly affected the global workforce and the global economy at large.

🃏

