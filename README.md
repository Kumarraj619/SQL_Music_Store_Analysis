# 🎵 Music Store SQL Analysis

## 📌 Overview
This project analyzes a music store database using SQL to extract insights about customer behavior, sales, genres, and artists.


---

## 🛠 Tools
- SQL (PostgreSQL)
- pgAdmin 4

---

## 🗂 Database Schema
![Schema](Schema.png)

---

## 📊 Key Analysis
- Identify top customers and highest revenue-generating cities  
- Analyze most popular genres by country  
- Find top-performing artists and tracks  
- Evaluate customer spending patterns  

---

## 🧾 Sample Query
```sql
WITH customer_spending AS (
    SELECT 
        c.country,
        c.customer_id,
        c.first_name || ' ' || c.last_name AS customer_name,
        SUM(i.total) AS total_spent
    FROM customer c
    JOIN invoice i ON c.customer_id = i.customer_id
    GROUP BY c.country, c.customer_id, c.first_name, c.last_name
),
ranked_customers AS (
    SELECT *,
           RANK() OVER (
               PARTITION BY country 
               ORDER BY total_spent DESC
           ) AS rnk
    FROM customer_spending
)
SELECT country, customer_name, total_spent
FROM ranked_customers
WHERE rnk = 1
ORDER BY country;

```

---

## 🚀 Future Work
- Add dashboards (Power BI)
- Optimize queries
- Expand analysis

---

## 🙌 Acknowledgement
Chinook Database (Sample dataset)
