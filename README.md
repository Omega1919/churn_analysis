# 📉 Customer Churn Analysis

## 📌 Project Overview

This project analyzes customer churn using the Superstore dataset. The goal is to identify inactive customers, understand churn behavior across customer segments and regions, and estimate the business revenue impact caused by customer churn.

The analysis was performed using SQL for data extraction and transformation, while the dashboard visualization was built using Google Looker Studio to provide interactive business insights.

---

# 📷 Dashboard Preview

![Churn Dashboard Preview](images/churn-dashboard.png)

🔗 **Interactive Dashboard:**  
https://datastudio.google.com/reporting/95049cc4-28bc-4d2b-a046-796531b22173

---

# 🛠️ Tools & Technologies Used

- SQL
- Google Looker Studio
- GitHub
- Superstore Dataset

---

# 📁 Project Structure

```bash
📦 customer-churn-analysis
 ┣ 📂 images
 ┃ ┗ 📜 churn-dashboard.png
 ┣ 📜 churn_analysis.sql
 ┣ 📜 README.md
 ┗ 📜 superstore_dataset.csv
```

---

# 📊 Business Objectives

The project aims to:

- Identify churned and at-risk customers
- Analyze churn trends across customer segments
- Evaluate regional churn performance
- Measure revenue loss caused by customer churn
- Provide business recommendations for customer retention

---

# 📊 Total Customer Count

## SQL Query

```sql
SELECT COUNT(customer_id) AS total_customer
FROM customer_churn;
```

## Result

| Total Customers |
|---|
| 793 |

## Insight

There are 793 unique customers across all orders in the dataset.

---

# 📊 Total Customers by Churn Status

## SQL Query

```sql
SELECT 
    churn_status,
    COUNT(customer_id) AS total_customer,
    ROUND(
        COUNT(customer_id) * 100 / 
        (SELECT COUNT(customer_id) FROM customer_churn),
        2
    ) AS total_percentage
FROM customer_churn
GROUP BY churn_status;
```

## Result

| Churn Status | Total Customers | Percentage |
|---|---|---|
| Churned | 436 | 54.98% |
| Active | 195 | 24.59% |
| At Risk | 162 | 20.43% |

## Insight

Churned customers account for nearly 55% of all customers, indicating a high customer inactivity rate.

At-risk customers represent over 20% of the customer base, meaning approximately 1 in every 5 customers may soon churn if no retention action is taken.

This suggests that customer retention campaigns should prioritize at-risk customers before they become fully inactive.

---

# 📊 Total Customers by Segment

## SQL Query

```sql
SELECT 
    segment,
    COUNT(customer_id) AS total_customer
FROM customer_metrics
GROUP BY segment
ORDER BY total_customer DESC;
```

## Result

| Segment | Total Customers |
|---|---|
| Consumer | 409 |
| Corporate | 236 |
| Home Office | 148 |

## Insight

The Consumer segment represents the largest customer group, making customer retention within this segment highly important for long-term revenue stability.

---

# 📊 Churn Rate by Region

## SQL Query

```sql
SELECT 
    region,
    SUM(CASE WHEN churn_status = 'churned' THEN 1 ELSE 0 END) 
    / COUNT(*) * 100.0 AS churn_percentage
FROM customer_metricss
GROUP BY region
ORDER BY churn_percentage DESC;
```

## Result

| Region | Churn Percentage |
|---|---|
| South | 59.09% |
| East | 57.69% |
| West | 48.48% |
| Central | 42.11% |

## Insight

The South and East regions show the highest churn rates, suggesting weaker customer retention performance compared to other regions.

These regions may benefit from:
- loyalty programs
- targeted marketing campaigns
- personalized offers
- customer engagement initiatives

---

# 📊 Total Churned Customers by Segment

## SQL Query

```sql
SELECT 
    segment,
    COUNT(churn_status) AS total_churn
FROM customer_metricss
WHERE churn_status = 'churned'
GROUP BY segment;
```

## Result

| Segment | Total Churn |
|---|---|
| Consumer | 215 |
| Corporate | 129 |
| Home Office | 92 |

## Insight

The Consumer segment has the highest number of churned customers, suggesting that improving customer loyalty within this segment could significantly reduce overall churn.

---

# 📊 Total Lost Revenue by Churned Customers

## SQL Query

```sql
SELECT 
    churn_status,
    SUM(total_sales) AS total_lost_revenue
FROM customer_churn
WHERE churn_status = 'churned'
GROUP BY churn_status;
```

## Result

| Churn Status | Total Lost Revenue |
|---|---|
| Churned | $1,149,286.65 |

## Insight

Churned customers account for over $1.14 million in lost revenue, highlighting the significant financial impact of customer inactivity on business performance.

---

# 📌 Key Findings

- More than half of customers are churned
- Consumer customers contribute the highest churn volume
- South and East regions experience the highest churn rates
- Churned customers generated over $1.14 million in lost revenue
- At-risk customers represent a major retention opportunity

---

# 📌 Business Recommendations

Based on the analysis, the following strategies are recommended:

- Focus retention campaigns on at-risk customers
- Improve customer engagement in high-churn regions
- Introduce loyalty programs for Consumer and Corporate customers
- Use discounts and personalized offers to reactivate inactive customers
- Continuously monitor churn metrics through dashboards

---

# 🧠 Conclusion

This churn analysis project provides insights into customer inactivity, regional churn patterns, and revenue loss caused by churned customers.

The analysis supports data-driven business decision-making and demonstrates how SQL and dashboard visualization tools can be used to solve real-world business problems.
