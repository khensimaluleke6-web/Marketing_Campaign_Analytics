Omnichannel Marketing Campaign & Consumer Behavior Analysis

## Project Overview
This end-to-end data analytics project provides an executive-level market research analysis using a dataset of 2,205 consumer profiles. The objective was to diagnose historic marketing campaign performance, uncover hidden demographic spending patterns and optimize purchasing channel budgets for an e-commerce brand.

## Tech Stack & Workflow
* Data Engineering & Cleaning:Google BigQuery (Cloud SQL)
* Visual Dashboarding & Analytics: Microsoft Excel (Pivot Tables, Dynamic Charts, Multi-Slicers)
* Data Pipeline Workflow: Cloud SQL Data Extraction ➔ Automated Transformation ➔ Excel Executive Reporting

---

## Core Business Insights Uncovered

### 1. Marketing Campaign Performance Matrix
* Campaign 1 (Wealth-Targeted Success): Achieved a massive 15.10% conversion rate exclusively within the High-Income bracket, but dropped to 0% for Low-Income buyers.
* Campaign 3 & 4 (Steady Workhorses): Generated well-balanced, multi-demographic engagement. Campaign 3 recorded a strong 11.11% success rate among Low-Level Education cohorts (likely driven by value-bundle promotions).
* Campaign 5 (Systemic Failure):Recorded a 0% response rate across all 2,205 records, signaling a complete strategy failure.

### 2. Behavioral Household Spending Habits
* The No-Children Multiplier:Households with no children act as the primary revenue engine, spending an average of $490 on Wine and $367 on Meat Products.
  
* The Small-Kids Contraction:Total basket size collapses by over 75% when small children are present in the home, before experiencing a moderate recovery as children mature into teenagers.

### 3. Omnichannel Purchase Preference
* Across every single age bracket, Physical Store Visits remain the dominant transaction medium, peaking heavily with the 44-53 age tier. 
* Direct-mail catalogs are obsolete, proving the business can safely reallocate that budget to digital ad spend.

```sql
SELECT Age,
CASE WHEN Income is NULL THEN 'Unknown'
WHEN Income  < 30000 THEN 'Low Income'
WHEN Income  <= 70000 THEN 'Medium Income'
ELSE 'High Income'
END AS Clean_Income_Group,   
CASE WHEN marital_married = 1 THEN 'Married'
WHEN marital_single = 1 THEN 'Single'
WHEN marital_together = 1 THEN 'Together'
WHEN marital_widow = 1 THEN 'Widow'
ELSE 'Unknown'<img width="1920" height="1080" alt="Screenshot 2026-06-28 220847" src="https://github.com/user-attachments/assets/1c851f45-af00-4dfe-93d3-77ffddcac91e" />
<img width="1920" height="1080" alt="Screenshot 2026-06-28 201610" src="https://github.com/user-attachments/assets/6912199a-48da-4ec8-997a-e612c85f872c" />
<img width="1920" height="1080" alt="Screenshot (31)" src="https://github.com/user-attachments/assets/aac747f7-8dfe-4df2-927a-60fd24691a73" />

END AS Clean_Marital_Status,
CASE WHEN education_Basic = 1 THEN 'Low Level Education'
WHEN 'education_2n Cycle' = 1 THEN 'Mid Level Education'
WHEN education_Graduation = 1 THEN 'Mid Level Education'
WHEN education_Master = 1 THEN 'Advanced (Masters)'
WHEN education_PhD = 1 THEN 'Advanced (PhD)'
ELSE 'Unknown'
END AS Clean_Education_Level,
CASE WHEN AcceptedCmp1 = 1 THEN 'Accepted' ELSE 'No Response' 
END AS Campaign_1,
CASE WHEN AcceptedCmp2 = 1 THEN 'Accepted' ELSE 'No Response' 
END AS Campaign_2,
CASE WHEN AcceptedCmp3 = 1 THEN 'Accepted' ELSE 'No Response' 
END AS Campaign_3,
CASE WHEN AcceptedCmp4 = 1 THEN 'Accepted' ElSE 'No Response' 
END AS Campaign_4,
CASE WHEN AcceptedCmp5 = 1 THEN 'Accepted' ELSE 'No Reponse' 
END AS Campaign_5,
CASE WHEN Kidhome > 0 AND Teenhome = 0 THEN 'Small kids only'
WHEN Kidhome = 0 AND Teenhome > 0 THEN 'Teenagers Only'
WHEN Kidhome > 0 AND Teenhome > 0 THEN 'Both kids and Teens'
ELSE 'No Children'
END AS Household_Type,
NumWebPurchases,
NumCatalogPurchases,
NumStorePurchases,
MntWines,
MntFruits,
MntFishProducts,
MntMeatProducts,
MntSweetProducts,
MntGoldProds,
FROM `graphite-dynamo-495620-d0.ifood.Marketing Analysis`
```
Query Table
<img width="1920" height="1080" alt="Screenshot 2026-06-25 140731" src="https://github.com/user-attachments/assets/5e00da46-9073-492b-9d41-badace0eb5e0" />

Campaign preference according to age, marital status, education level and income groups.
<img width="1920" height="1080" alt="Screenshot 2026-06-28 201610" src="https://github.com/user-attachments/assets/da0cf84c-d7fd-4720-8213-3a10489fd3ac" />

Pivot Table and Slicers
<img width="1920" height="1080" alt="Screenshot (31)" src="https://github.com/user-attachments/assets/8759ab3e-062d-4668-9326-5651a978526c" />

Purchase Medium Preference
<img width="1920" height="1080" alt="Screenshot 2026-06-28 214028" src="https://github.com/user-attachments/assets/7e15197e-a06d-4a79-bebf-df4619fa3ef2" />
