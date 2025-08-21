# Industry-Carbon-Emissions
This project analyzes industry-level carbon emissions using SQL to identify key contributors, trends, and hotspots. It provides insights into environmental impact and supports data-driven strategies for sustainable and greener industrial practices.

## Project Overview

This project analyzes Product Carbon Footprints (PCFs) for companies across various industries, using the ```product_emissions``` table to identify the number of unique companies and their total carbon footprint for each industry group, focusing on the most recent year in the dataset.

PCFs represent the greenhouse gas emissions generated throughout the lifecycle of products—from raw material extraction and production to transportation and disposal—measured in CO₂ equivalents. Greenhouse gas emissions generated throughout product lifecycles account for more than 75% of global emissions (Source: The Carbon Catalogue, Nature Article).

By analyzing these footprints, the project provides insight into how emissions are distributed across industries, companies, and product categories, offering a clearer view of the sectors driving the highest environmental impact.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Objectives / Key Questions
* Determine the range of years covered in the dataset.  
* Understand the structure and types of data in the table.  
* Identify the total carbon footprint per industry since 2017.  

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Dataset

* **Source**: The Carbon Catalogue https://www.nature.com/articles/s41597-022-01178-9  
* **Table**: `product_emissions`  
* **Structure**:

| Field                        | Data Type |  
|-------------------------------|-----------|  
| id                            | VARCHAR   |  
| year                          | INT       |  
| product_name                  | VARCHAR   |  
| company                       | VARCHAR   |  
| country                       | VARCHAR   |  
| industry_group                | VARCHAR   |  
| weight_kg                     | NUMERIC   |  
| carbon_footprint_pcf          | NUMERIC   |  
| upstream_percent_total_pcf    | VARCHAR   |  
| operations_percent_total_pcf  | VARCHAR   |  
| downstream_percent_total_pcf  | VARCHAR   |  

* **Sample Preview**:

```
sql

SELECT *
FROM product_emissions
LIMIT 10;
```
This query retrieves the first 10 rows of the `product_emissions` table to provide a snapshot of the data, allowing us to verify the dataset’s structure, check column values, and get a preliminary understanding of the information captured for each product, company, and industry.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Tools & Skills Used

* **SQL (PostgreSQL) Concepts**: ```SELECT, DISTINCT, COUNT, SUM, MAX, MIN, ROUND, GROUP BY, ORDER BY, WHERE, LIMIT```
* **Techniques Used**: Data exploration, understanding data types, aggregation, filtering, rounding values, summarizing emissions per industry

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Analysis & Approach

### 1. Exploring the Data

```
sql

SELECT *
FROM product_emissions;
```
This query retrieves the entire dataset to examine all rows and columns. It helps understand the range of products, companies, industries, and recorded carbon footprints, providing a full picture of the data before deeper analysis.

<img width="1220" height="629" alt="image" src="https://github.com/user-attachments/assets/b894e614-cf52-4295-b8fa-3be1e6abb6ac" />



### 2. Understanding Datatypes

```
sql

SELECT column_name, data_type
FROM information_schema.columns
WHERE table_name = 'product_emissions';
```
This query lists all columns in the `product_emissions` table along with their data types. It ensures numerical fields such as carbon_footprint_pcf and weight_kg are correctly typed, and categorical fields like industry_group and company are properly recognized for grouping and analysis.

<img width="1221" height="449" alt="image" src="https://github.com/user-attachments/assets/3fcb9b45-d5ba-435f-978e-04fc2ca664e1" />



### 3. Determining Dataset Year Range

```
sql

SELECT
    MAX(year) AS max_years,
    MIN(year) AS min_years
FROM product_emissions;
```
This query identifies the earliest and latest years represented in the dataset. Knowing the temporal range of the data helps contextualize trends and ensures that subsequent analysis (e.g., industry-level summaries since 2017) focuses on relevant years.

<img width="1221" height="119" alt="image" src="https://github.com/user-attachments/assets/26e5bea8-61be-4594-9f0e-486bd23746d5" />



### 4. Carbon Emissions by Industry

```
sql

SELECT
    industry_group,
    COUNT(DISTINCT company) AS num_companies, 
    ROUND(SUM(carbon_footprint_pcf), 1) AS total_industry_footprint 
FROM product_emissions
WHERE year >= 2017
GROUP BY industry_group
ORDER BY total_industry_footprint DESC;
```
This analysis measures total carbon emissions per industry from 2017 onwards. It identifies how many unique companies contribute within each sector and highlights the overall carbon footprint of their products, providing a clear view of industry-level environmental impact.

<img width="1215" height="287" alt="image" src="https://github.com/user-attachments/assets/ae69d5f6-96d8-41e2-a08f-3afe24853f84" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Insights & Findings

* **Industry-level variation**: The results show that carbon emissions are not evenly distributed across industries—some sectors produce significantly higher emissions than others, indicating where sustainability efforts and regulatory policies could have the greatest impact.
* **Company participation**: The number of companies within each industry also varies; industries with more companies may contribute higher overall emissions, but in some cases, a smaller number of companies are responsible for disproportionately large carbon footprints, pointing to potential outliers or heavy emitters.
* **Focus on recent years**: By limiting the analysis to 2017 onward, the results emphasize a more contemporary picture of industrial emissions, making it possible to identify which industries are currently the largest contributors to carbon footprints and where immediate action is most needed.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Final Notes

This project demonstrates how SQL can be used to analyze product carbon footprints at an industry level. By aggregating emissions, counting unique companies, and filtering by relevant years, we gain insight into which industries contribute most to global carbon emissions. Such analysis can inform environmental policy, corporate sustainability strategies, and consumer awareness regarding the carbon impact of products.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------















