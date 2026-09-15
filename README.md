# FMCG-_SALES_MARKETING-2023---2025-ANALYSIS
# FMCG SALES, MARKETING & PROFITABILITY ANALYSIS

## TABLE OF CONTENTS

1. [Background](#background)
2. [Data Structure](#data-structure)

   * [Data Model](#data-model)
   * [Data Pipeline](#data-pipeline)
3. [Executive Summary](#executive-summary)
4. [Insights Deep Dive](#insights-deep-dive)
5. [Recommendations](#recommendations)
6. [Assumptions and Caveats](#assumptions-and-caveats)
7. [Next Steps](#next-steps)
8. [About](#about)
9. [Resources](#resources)

---

## BACKGROUND

The Fast-Moving Consumer Goods (FMCG) industry operates in a highly competitive environment where businesses must continuously balance sales growth, customer demand, product performance, marketing investment, operating costs, and profitability.

For this analysis, I worked with an FMCG sales and marketing dataset sourced from **Kaggle**, covering transactional activity from **2023 to 2025**. The dataset contains **18,240 records across 27 fields**, providing information on orders, products, brands, customers, geographic markets, promotion types, marketing spend, sales, costs, revenue, and profit.

The objective of this analysis is to evaluate the company's sales and commercial performance, identify the products, brands, and markets driving demand, examine how marketing investment is distributed, and assess the relationship between marketing spend and profitability.

This project combines **PostgreSQL, SQL, Power BI, and DAX** to move from data validation and analytical querying to interactive business intelligence and insight generation.

### Key Business Questions

To address the key performance areas, the analysis focuses on the following questions:

1. **Sales Performance:** How did sales grow across 2023–2025?
2. **Geographic Performance:** Which country recorded the highest purchase volume?
3. **Product Performance:** Which product was sold the most?
4. **Brand Performance:** Which brand generated the highest sales?
5. **Promotion Performance:** Which promotion type generated the highest revenue?
6. **Marketing Investment:** Which promotion type received the highest marketing spend?
7. **Geographic Marketing Investment:** Which countries received the most marketing investment?
8. **Marketing & Profitability:** What is the relationship between marketing spend and profit?
# 2. DATA STRUCTURE

## Data Model

The analysis is based on a single transactional FMCG dataset containing **18,240 records and 27 columns**. Each record represents an individual order and contains information covering the order date, location, customer, product, promotion, sales activity, marketing investment, costs, revenue, and profitability.

The dataset can be organized into the following analytical dimensions:

### 1. Order & Time

| Field        | Description                     |
| ------------ | ------------------------------- |
| `Order_ID`   | Unique identifier for the order |
| `Order_Date` | Date the order was placed       |
| `Year`       | Year of the transaction         |
| `Quarter`    | Quarter of the transaction      |
| `Month`      | Numerical month                 |
| `Month_Name` | Name of the month               |

### 2. Geography

| Field     | Description                       |
| --------- | --------------------------------- |
| `Region`  | Geographic region                 |
| `Country` | Country associated with the order |
| `City`    | City associated with the order    |

### 3. Customer & Sales

| Field           | Description             |
| --------------- | ----------------------- |
| `Sales_Person`  | Sales representative    |
| `Customer_Type` | Customer classification |
| `Sales_Channel` | Sales channel used      |

### 4. Product

| Field              | Description        |
| ------------------ | ------------------ |
| `Product_Category` | Product category   |
| `Brand`            | Product brand      |
| `Product_Name`     | Individual product |
| `SKU`              | Stock-keeping unit |

### 5. Marketing & Promotion

| Field                 | Description                 |
| --------------------- | --------------------------- |
| `Promotion_Type`      | Promotion/campaign category |
| `Marketing_Spend_USD` | Marketing expenditure       |
| `Discount_Pct`        | Discount percentage         |

### 6. Sales & Financial Performance

| Field                | Description              |
| -------------------- | ------------------------ |
| `Units_Sold`         | Number of units sold     |
| `Unit_Price_USD`     | Price per unit           |
| `Gross_Sales_USD`    | Gross sales generated    |
| `COGS_USD`           | Cost of goods sold       |
| `Logistics_Cost_USD` | Logistics cost           |
| `Net_Revenue_USD`    | Net revenue              |
| `Profit_USD`         | Profit generated         |
| `Profit_Margin_Pct`  | Profit margin percentage |

### Data Relationships

The dataset allows performance to be analyzed across multiple dimensions.

For example:

* **Year → Sales** to evaluate growth over time
* **Country → Units Sold** to evaluate purchase volume
* **Product → Units Sold** to identify high-demand products
* **Brand → Sales** to compare brand performance
* **Promotion Type → Sales** to evaluate revenue performance
* **Promotion Type → Marketing Spend** to examine investment allocation
* **Country → Marketing Spend** to compare geographic investment
* **Marketing Spend → Profit** to examine the relationship between marketing investment and profitability

This structure provides a single analytical view of the relationship between **commercial activity, marketing investment, and financial performance**.

## Data Quality Checks

Before performing the analysis, the dataset was validated using SQL in PostgreSQL.

The validation covered:

* Completeness of key fields
* Duplicate order identification
* Numerical range checks
* Gross sales calculation validation
* Negative-profit transaction review

The `Gross_Sales_USD` field was validated against the relationship:

**Units Sold × Unit Price = Gross Sales**

The validation returned **0 incorrect records**, confirming consistency between the underlying sales quantity, unit price, and gross sales values.

Duplicate checking also identified **no duplicate Order_ID records**.

Negative-profit transactions were retained because they represent legitimate business outcomes and are relevant when evaluating profitability rather than being treated as data errors.
## Data Pipeline

The analysis followed a structured workflow that moved the dataset from its original Kaggle source through SQL-based validation and analysis before being developed into an interactive Power BI dashboard.

### 1. Data Source

The dataset was obtained from **Kaggle** in CSV format.

It contains **18,240 transaction records and 27 columns**, covering FMCG sales, marketing, cost, revenue, and profitability information from **2023 to 2025**.

### 2. PostgreSQL

The CSV dataset was imported into **PostgreSQL**, where the data was stored in the `fmcg_sales` table.

PostgreSQL was used as the primary SQL environment for:

* Inspecting the dataset
* Validating data quality
* Checking for duplicate records
* Validating numerical fields
* Verifying gross sales calculations
* Performing analytical SQL queries

### 3. SQL Analysis

SQL was used to investigate the underlying data before building the dashboard.

The analysis included yearly sales aggregation and year-over-year growth calculations using:

* Common Table Expressions (CTEs)
* Aggregate functions such as `SUM()`
* The `LAG()` window function
* Conditional and validation queries

The SQL stage established confidence in the underlying data and provided an analytical foundation for the Power BI stage.

### 4. Power BI

The validated dataset was loaded into **Power BI** for interactive business analysis.

The dashboard was developed on a **16:9 canvas** and combines summary metrics with detailed analytical visuals.

The report contains:

* **5 KPI cards**
* **8 analytical visuals**
* **3 interactive slicers**

### 5. DAX

DAX measures were created to support dynamic calculations within Power BI.

The measures include:

* `Total Sales`
* `Total Profit`
* `Total Units Sold`
* `Total Marketing Spend`
* `Profit Margin`

The measures allow the dashboard metrics to recalculate dynamically when users filter the report.

### 6. Dashboard & Business Analysis

The final dashboard brings together sales, product, brand, geographic, marketing, and profitability analysis.

Interactive slicers for **Year, Region, and Promotion Type** allow users to explore the results from different business perspectives.

The completed workflow can therefore be summarized as:

**Kaggle → CSV → PostgreSQL → SQL Validation & Analysis → Power BI → DAX → Interactive Dashboard**
# 3. EXECUTIVE SUMMARY

## Overview

The analysis of **18,240 FMCG transactions** from 2023–2025 generated a total of **$17.08 million in gross sales**, **$3.31 million in profit**, and **3.88 million units sold**. Total marketing expenditure over the period was **$1.56 million**, while the overall profit margin was **19.37%**.

Overall sales increased throughout the three-year period, although the pace of growth slowed in 2025.

### Sales Growth

| Year | Gross Sales | Year-over-Year Growth |
| ---- | ----------: | --------------------: |
| 2023 |      $5.43M |                     — |
| 2024 |      $5.73M |             **5.49%** |
| 2025 |      $5.92M |             **3.43%** |

Sales grew by approximately **9.10%** between 2023 and 2025. However, the reduction in annual growth from **5.49% in 2024 to 3.43% in 2025** indicates a slowing growth trajectory that may require further investigation.

### Key Performance Highlights

**USA led purchase volume**, recording **434,110 units sold**, followed by India with 375,836 units.

**Energy Drink Zero was the highest-volume product**, with **198,116 units sold**, making it the leading product by purchase volume.

**HomeNest generated the highest brand sales**, recording approximately **$1.62 million** in gross sales.

Among the promotion categories, **No Promo recorded the highest gross sales at $6.30 million**. This result should be interpreted carefully because "No Promo" represents transactions without a named promotion and may reflect the underlying base sales volume rather than the performance of an active marketing campaign.

The dataset also recorded the highest marketing expenditure under **No Promo**, at approximately **$452,422**.

The **USA received the highest marketing investment**, with approximately **$187,214** in marketing spend.

### Marketing & Profitability

Marketing spend and profit showed a **moderate positive relationship**, with a Pearson correlation of approximately **0.512** across the transaction records.

This indicates that higher marketing expenditure tends to be associated with higher profit in the observed data. However, correlation does **not** establish that increased marketing spend directly causes higher profit.

The dataset also contained **784 negative-profit transactions**. These records were retained because they represent valid business outcomes and provide useful information when evaluating profitability and cost performance.

### Overall Business Picture

The analysis indicates that the business experienced **continued sales and profit growth between 2023 and 2025**, supported by strong demand across several products and markets.

At the same time, the slower sales growth in 2025, concentration of purchase volume and marketing investment in certain countries, and the presence of negative-profit transactions highlight areas where deeper performance and investment analysis could support better decision-making.
# 4. INSIGHTS DEEP DIVE

## 4.1 Sales Performance

### Sales Growth Across 2023–2025

Total gross sales increased consistently across the three-year period:

* **2023:** $5.43M
* **2024:** $5.73M
* **2025:** $5.92M

Sales increased by **5.49%** from 2023 to 2024 and by **3.43%** from 2024 to 2025.

Although the business continued to grow, the decline in the year-over-year growth rate suggests that sales momentum slowed in 2025.

**Business implication:** Continued growth is positive, but the slower growth rate suggests that the business may need to identify the products, markets, customers, or commercial activities responsible for sustaining future growth.

---

## 4.2 Geographic Performance

### Purchase Volume by Country

The **United States recorded the highest purchase volume**, with **434,110 units sold**.

The next highest-volume markets were:

| Rank | Country   |  Units Sold |
| ---: | --------- | ----------: |
|    1 | USA       | **434,110** |
|    2 | India     |     375,836 |
|    3 | Germany   |     275,349 |
|    4 | UK        |     271,509 |
|    5 | Australia |     256,526 |

The difference between the USA and the second-highest market, India, indicates particularly strong unit demand in the USA.

**Business implication:** The USA represents an important demand market. Its strong purchase volume makes it a key market for understanding customer behavior, product preferences, and marketing effectiveness.

---

## 4.3 Product Performance

### Top Products by Units Sold

**Energy Drink Zero** was the highest-volume product, with **198,116 units sold**.

The leading products were:

| Rank | Product              |  Units Sold |
| ---: | -------------------- | ----------: |
|    1 | Energy Drink Zero    | **198,116** |
|    2 | Energy Drink Classic |     180,188 |
|    3 | Protein Bar Cocoa    |     159,195 |
|    4 | Instant Coffee Gold  |     159,112 |
|    5 | Chocolate Cookies    |     158,395 |

Energy Drink Zero sold approximately **17,928 more units than Energy Drink Classic**, the second-highest-volume product.

**Business implication:** High-volume products such as Energy Drink Zero should receive close attention when evaluating inventory planning, availability, pricing, and profitability.

However, unit volume alone does not determine whether a product is the most profitable. A deeper product-margin analysis would be required to make that conclusion.

---

## 4.4 Brand Performance

### Sales by Brand

**HomeNest** generated the highest gross sales among the brands, with approximately **$1.62 million**.

The leading brands by sales were:

| Rank | Brand      | Gross Sales |
| ---: | ---------- | ----------: |
|    1 | HomeNest   |  **$1.62M** |
|    2 | PureLiva   |      $1.56M |
|    3 | FuelCore   |      $1.48M |
|    4 | RoastTrail |      $1.38M |
|    5 | MorningCo  |      $1.16M |

HomeNest therefore led the brand-level sales performance during the period analyzed.

**Business implication:** HomeNest represents an important contributor to overall sales. Its product mix, pricing, demand patterns, and profitability could be investigated further to understand what is driving its strong performance.

---

## 4.5 Promotion & Revenue Performance

### Revenue by Promotion Type

Among the promotion categories in the dataset, **No Promo recorded the highest gross sales**, generating approximately **$6.30 million**.

The other major categories included:

| Promotion Type     | Gross Sales |
| ------------------ | ----------: |
| No Promo           |  **$6.30M** |
| Bundle Offer       |      $2.69M |
| Seasonal Campaign  |      $2.65M |
| Flash Discount     |      $2.00M |
| Festival Campaign  |      $1.46M |
| Loyalty Cashback   |      $1.31M |
| Introductory Offer |      $0.68M |

The large sales figure associated with No Promo should not be interpreted as evidence that promotional activity is ineffective. It represents sales transactions without a named promotion and may reflect the business's underlying base demand.

**Business implication:** Promotion performance should ideally be evaluated using additional measures such as incremental sales, profit margin, and return on marketing investment rather than gross sales alone.

---

## 4.6 Marketing Investment by Promotion Type

### Marketing Spend by Promotion Type

The largest recorded marketing expenditure was associated with **No Promo**, at approximately **$452,422**.

This was followed by:

* Seasonal Campaign — **$266,508**
* Bundle Offer — **$259,856**
* Flash Discount — **$236,780**
* Festival Campaign — **$178,390**

The presence of substantial marketing spend under the No Promo category is noteworthy.

**Business implication:** The business should verify how baseline or always-on marketing expenditure is classified in the source data. If the category represents ongoing marketing activity rather than zero promotional activity, the classification should be clarified before using it for campaign-level budget decisions.

---

## 4.7 Marketing Investment by Country

### Marketing Spend Across Countries

The **USA received the highest marketing investment**, with approximately **$187,214**.

The leading markets by marketing spend were:

| Rank | Country   | Marketing Spend |
| ---: | --------- | --------------: |
|    1 | USA       |    **$187,214** |
|    2 | Germany   |        $124,740 |
|    3 | UK        |        $121,879 |
|    4 | India     |        $120,908 |
|    5 | Australia |        $117,098 |

The USA therefore ranked highest in both **purchase volume** and **marketing investment**.

**Business implication:** The alignment between high demand and high marketing investment in the USA makes it an important market for evaluating marketing efficiency and return on investment.

---

## 4.8 Marketing Spend & Profitability

### Relationship Between Marketing Spend and Profit

A scatter analysis was used to examine the relationship between marketing expenditure and profit.

The Pearson correlation between marketing spend and profit was approximately **0.512**, indicating a **moderate positive relationship**.

In general, records with higher marketing expenditure tended to be associated with higher profit. However, this relationship should not be interpreted as proof that marketing spend directly causes higher profit.

Profit is influenced by multiple factors, including:

* Sales
* Product pricing
* Discounts
* Cost of goods sold
* Logistics costs
* Marketing expenditure

### Negative-Profit Transactions

The dataset contains **784 transactions with negative profit**.

These records were retained because negative profit is a valid business outcome and can reveal transactions where the associated costs outweighed the profit generated.

**Business implication:** Negative-profit transactions should be investigated further to identify whether they are concentrated around particular products, countries, promotion types, customer types, or sales channels.

---

## Key Insight

The overall analysis shows a business with **positive sales growth and profitability**, but with several areas requiring closer performance monitoring.

The strongest themes emerging from the analysis are:

1. Sales continued to grow, but growth slowed in 2025.
2. The USA was the leading market by purchase volume and marketing investment.
3. Energy Drink Zero was the highest-volume product.
4. HomeNest was the highest-selling brand.
5. No Promo recorded the highest gross sales and marketing spend, requiring careful interpretation.
6. Marketing spend had a moderate positive relationship with profit.
7. Negative-profit transactions highlight opportunities for deeper cost and profitability analysis.
# 5. RECOMMENDATIONS

The following recommendations are derived from the sales, product, geographic, marketing, and profitability findings identified in the analysis.

## Immediate Actions

### 1. Investigate the slowdown in sales growth

Sales increased from **$5.43M in 2023 to $5.92M in 2025**, but year-over-year growth declined from **5.49% in 2024 to 3.43% in 2025**.

Management should investigate which products, countries, customer types, and sales channels contributed to the slowdown and identify areas capable of sustaining future growth.

### 2. Review the "No Promo" classification

"No Promo" recorded both the highest gross sales (**$6.30M**) and the highest marketing spend (**$452,422**).

The business should verify whether this category represents genuinely non-promotional sales or ongoing/always-on marketing expenditure. Clarifying this classification is important before using the data to make campaign-level budget decisions.

### 3. Investigate negative-profit transactions

There are **784 negative-profit transactions** in the dataset.

These transactions should be segmented by product, country, promotion type, customer type, and sales channel to identify recurring sources of loss.

---

## Short-Term Actions

### 4. Evaluate the USA market's marketing efficiency

The USA recorded the highest purchase volume at **434,110 units** and also received the highest marketing investment at approximately **$187,214**.

Management should compare the level of investment with the profit generated in the market to determine whether the high spending is translating into proportionate business returns.

### 5. Monitor high-volume products

**Energy Drink Zero** was the highest-volume product, with **198,116 units sold**.

The business should monitor its inventory availability, pricing, sales trends, and profitability to ensure that strong demand is being converted into sustainable financial performance.

### 6. Examine the performance of leading brands

**HomeNest** generated approximately **$1.62M in gross sales**, making it the highest-selling brand.

A deeper review of HomeNest's product mix and margins could identify the factors driving its strong sales performance and whether the performance is equally strong at the profit level.

---

## Medium-Term Actions

### 7. Develop promotion-level profitability analysis

Gross sales alone do not establish whether a promotion is financially successful.

The business should evaluate promotion types using a combination of:

* Gross sales
* Net revenue
* Profit
* Marketing spend
* Profit margin
* Return on marketing investment

This would provide a stronger basis for deciding which campaigns should receive additional funding.

### 8. Optimize geographic marketing allocation

Marketing investment is concentrated among several major markets, with the USA receiving the highest spend.

Management should compare marketing expenditure against sales and profit by country to identify markets where additional investment could generate stronger returns and markets where spending may need to be optimized.

### 9. Monitor marketing spend against profitability

The observed correlation of approximately **0.512** suggests a moderate positive relationship between marketing spend and profit.

Rather than increasing marketing expenditure solely because of this relationship, the business should conduct more detailed ROI analysis to determine which types of marketing investment contribute most effectively to profitable growth.

---

## Long-Term Actions

### 10. Build a marketing ROI monitoring framework

Future reporting should track marketing effectiveness using standardized measures such as:

* Marketing Spend
* Incremental Revenue
* Profit Contribution
* Return on Marketing Investment
* Profit Margin

This would allow management to move from monitoring expenditure to measuring the financial return generated by marketing activity.

### 11. Develop a recurring performance dashboard

The Power BI dashboard developed in this project can serve as a foundation for ongoing monitoring.

A recurring reporting process could track:

* Sales growth
* Product demand
* Brand performance
* Geographic performance
* Marketing investment
* Profitability
* Negative-profit transactions

This would help management identify changes in performance earlier and support data-driven decision-making.
# 6. ASSUMPTIONS AND CAVEATS

The following assumptions and limitations were considered when interpreting the analysis.

### 1. Dataset Source

The dataset was obtained from **Kaggle**. The analysis therefore relies on the information and definitions provided within the dataset and does not independently verify the original business context behind each transaction.

### 2. Gross Sales vs. Net Revenue

The analysis of sales performance primarily uses **Gross_Sales_USD** because it directly represents the sales value used in the defined business question.

Gross sales should not be interpreted as equivalent to the company's final realized revenue or cash received. The dataset also contains `Net_Revenue_USD`, which should be considered when conducting a deeper financial analysis.

### 3. Negative Profit

The dataset contains **784 transactions with negative profit**.

These records were retained because negative profit represents a legitimate business outcome rather than a data-quality error. Removing them would potentially hide important information about loss-making transactions.

### 4. "No Promo" Classification

`No Promo` recorded both the highest gross sales and the highest marketing spend.

This result requires careful interpretation because marketing expenditure appearing under a "No Promo" category may represent baseline, always-on, or otherwise unclassified marketing activity.

Therefore, the analysis does not conclude that "No Promo" is inherently the most effective marketing strategy.

### 5. Marketing Spend and Profit Relationship

The correlation between marketing spend and profit was approximately **0.512**.

This indicates a moderate positive association within the observed records, but correlation does not establish causation.

Higher marketing expenditure cannot automatically be interpreted as the cause of higher profit because profitability is affected by multiple factors, including sales, pricing, discounts, COGS, logistics costs, and other business variables.

### 6. Product Performance

The product analysis uses **units sold** to answer the purchase-volume question.

A product with the highest unit volume is not necessarily the most profitable product. Profitability would require additional analysis of revenue and associated costs at the product level.

### 7. Brand Performance

Brands were ranked using **Gross Sales**, as defined by the business question.

The highest-selling brand is therefore not automatically the highest-profit brand.

### 8. Marketing Efficiency

The analysis identifies where marketing spend was concentrated but does not establish a definitive return on investment for each campaign or country.

A more comprehensive marketing effectiveness study would require measures such as incremental sales, campaign attribution, customer acquisition cost, or return on marketing investment.

### 9. Historical Analysis

The analysis covers the period **2023–2025**. The findings describe performance within this period and should not automatically be assumed to represent future performance.

### 10. Scope of the Analysis

The project focuses on the eight defined business questions. Additional dimensions such as customer profitability, sales-channel efficiency, product-level margins, and detailed cost contribution could provide further insights in a future analysis.
# 7. NEXT STEPS

The current analysis provides a foundation for monitoring sales, marketing investment, and profitability. The following areas could be explored to extend the analysis and support more advanced business decision-making.

### 1. Product-Level Profitability Analysis

Extend the analysis beyond units sold to identify which products generate the highest profit and profit margins.

This would help distinguish between products that sell in high volumes and products that create the greatest financial contribution.

### 2. Customer Profitability Analysis

Analyze profitability by `Customer_Type` and individual customers to identify high-value customer segments and potentially loss-making customer groups.

### 3. Sales Channel Performance

Compare sales, profit, units sold, and marketing investment across `Sales_Channel` to determine which channels deliver the strongest commercial performance.

### 4. Promotion ROI Analysis

Develop a more detailed promotion-performance framework using:

* Marketing spend
* Gross sales
* Net revenue
* Profit
* Profit margin
* Return on marketing investment

This would allow future analysis to move beyond measuring sales generated by promotions toward measuring their financial effectiveness.

### 5. Geographic Profitability

The current analysis identifies countries with the highest purchase volume and marketing investment. A future analysis should compare these markets by **profit and profit margin** to determine whether high-demand and high-investment markets are also the most profitable.

### 6. Investigate Negative-Profit Transactions

The **784 negative-profit transactions** should be analyzed further to determine whether losses are concentrated around specific:

* Products
* Countries
* Promotion types
* Customer types
* Sales channels

Identifying recurring patterns could help reduce avoidable losses.

### 7. Marketing Attribution

A future analysis could incorporate campaign-level or customer-level attribution data to better determine how marketing activity contributes to sales and profit.

This would provide stronger evidence for marketing budget allocation than correlation alone.

### 8. Automated Reporting

The Power BI dashboard could be connected to a regularly refreshed data source to create an ongoing performance-monitoring system.

Future reporting could track changes in:

* Sales growth
* Profitability
* Product demand
* Marketing spend
* Promotion performance
* Geographic performance

This would transform the current analysis from a historical report into a recurring business intelligence solution.
# 8. ABOUT

This project demonstrates an end-to-end data analytics workflow applied to FMCG sales, marketing, and profitability data from 2023–2025.

Using **PostgreSQL, SQL, Power BI, and DAX**, the analysis transforms transactional data into business insights across sales growth, geographic demand, product and brand performance, marketing investment, promotion performance, and profitability.

The project demonstrates practical skills in:

* SQL data validation and analysis
* Data quality assessment
* Business question development
* DAX measure creation
* Power BI dashboard development
* Data storytelling
* Business insight generation
* Data-driven recommendations
# 9. RESOURCES

### Dataset

* **Source:** Kaggle
* **Dataset:** FMCG Sales, Marketing & Profitability dataset covering 2023–2025
* **Records:** 18,240
* **Columns:** 27

### Tools & Technologies

* **PostgreSQL** — database management, data validation, and SQL analysis
* **SQL** — data quality checks, aggregation, validation, and analytical queries
* **Power BI** — interactive dashboard development and data visualization
* **DAX** — dynamic measures and business calculations

### Project Deliverables

The project repository contains the analytical resources associated with the project, including:

* Dataset
* SQL queries
* Power BI dashboard
* Project documentation
* Dashboard screenshots/visual assets where applicable

