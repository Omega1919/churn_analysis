# 📉 Churn Customer Analysis

## 📌 Project Overview

This project analyzes customer churn using the Superstore dataset. The goal is to identify inactive customers, understand churn behavior across regions and customer segments, and estimate the revenue impact caused by customer churn.

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

Churned customers have the highest number of customers, accounting for nearly 55% of all customers who have been inactive for more than 60 days.

At-risk customers represent over 20% of total customers, meaning about 1 in every 5 customers may soon become churned if no action is taken.

This suggests that retention campaigns, discounts, and customer engagement strategies should focus on at-risk customers before they become fully inactive.

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

The Consumer segment has the highest number of customers, making up more than half of the customer base.

Corporate customers follow behind, while Home Office customers represent the smallest customer segment.

This indicates that the business relies heavily on consumer customers, making customer retention within this segment especially important.

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

The South region has the highest churn rate at 59%, followed closely by the East region at 58%.

More than half of customers in these regions have become inactive.

This suggests that retention offers, loyalty programs, discounts, and targeted customer engagement campaigns may help reduce customer churn in these regions.

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

The Consumer segment has the highest number of churned customers with 215 inactive customers.

This may be caused by lower customer loyalty and a higher number of one-time buyers within the segment.

The Corporate segment also shows a significant number of churned customers, suggesting that retention campaigns and personalized offers may help improve customer retention across both segments.

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

Churned customers account for over $1.14 million in lost revenue, representing a significant portion of total business revenue.

This highlights the importance of improving customer retention strategies, especially for at-risk customers, before they become fully churned customers.

---

# 📌 Final Business Recommendations

Based on the analysis, the following actions are recommended:

- Focus retention campaigns on at-risk customers before they become churned
- Improve customer engagement strategies in South and East regions
- Introduce loyalty programs for Consumer and Corporate customer segments
- Use discounts and personalized offers to reactivate inactive customers
- Monitor churn trends regularly to reduce future revenue loss

---

# 🧠 Conclusion

This churn analysis provides insights into customer inactivity, revenue loss, and regional churn behavior.

The analysis helps businesses identify high-risk customer groups and supports data-driven decision-making for improving customer retention and long-term business performance.
