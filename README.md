# ABC Orders — SQL Data Analysis

## 📌 Project Overview

This project analyzes the **ABC Orders** database using SQL after performing data cleaning and transformation.
The objective is to extract business insights related to revenue, product performance, pricing strategy, and operational efficiency.

---

## 🧹 Data Preparation Steps

1. Converted `order_date` and `ship_date` to DATE format.
2. Checked for NULL values in key columns.
3. Identified duplicate order numbers.
4. Standardized table structure for analysis.

---

## 📊 Key Analysis Performed

### 1️⃣ Business Performance Summary

Measures overall business scale.

```sql
SELECT 
    COUNT(DISTINCT order_no) AS total_orders,
    SUM(sales) AS total_revenue,
    SUM(profit) AS total_profit,
    AVG(profit) AS avg_profit_per_order
FROM orders;
```

**Insight:** Provides a snapshot of company performance.

---

### 2️⃣ Revenue by Product Category

Identifies which product segments generate the most revenue.

```sql
SELECT product_category, 
       ROUND(SUM(total), 2) AS Revenue
FROM orders
JOIN products
ON orders.product_id = products.product_id
GROUP BY product_category;
```

**Insight:** Shows revenue distribution across categories.

---

### 3️⃣ Yearly Revenue Analysis

Tracks business performance over time.

```sql
SELECT EXTRACT(YEAR FROM order_date) AS Year,
       ROUND(SUM(total), 2) AS Revenue
FROM orders
GROUP BY Year
ORDER BY Year;
```

**Insight:** Reveals growth trends year by year.

---

### 4️⃣ Lowest Average Price Category

Finds the most budget-friendly product category.

```sql
SELECT product_category,
       ROUND(AVG(retail_price), 2) AS Average_price
FROM orders
JOIN products USING(product_id)
GROUP BY product_category
ORDER BY Average_price
LIMIT 1;
```

**Insight:** Identifies the category with the lowest pricing level.

---

### 5️⃣ Shipping Performance Analysis

Evaluates delivery efficiency.

```sql
SELECT 
    MIN(DATEDIFF(ship_date, order_date)) AS fastest_shipping,
    MAX(DATEDIFF(ship_date, order_date)) AS slowest_shipping,
    AVG(DATEDIFF(ship_date, order_date)) AS avg_shipping_days
FROM orders;
```

**Insight:** Measures operational logistics performance.

---

### 6️⃣ Profitability Analysis

Assesses financial health of the business.

```sql
SELECT 
    SUM(sales) AS total_sales,
    SUM(profit) AS total_profit,
    ROUND((SUM(profit) / SUM(sales)) * 100, 2) AS profit_margin_percent
FROM orders;
```

**Insight:** Indicates how efficiently revenue converts to profit.

---

## 🧠 Key Findings (Example Interpretation)

* Certain product categories dominate revenue contribution.
* Business shows measurable yearly growth.
* Some orders generate negative profit, indicating cost or discount issues.
* Shipping performance varies and affects operational efficiency.

---

## 🛠️ Tools Used

* MySQL
* SQL Joins
* Aggregate Functions
* Date Functions
* Data Cleaning Techniques

---

## 🎯 Project Outcome

This analysis provides decision-support insights for:

* Product strategy
* Pricing optimization
* Operational improvement
* Revenue growth planning

---

## 📁 Dataset Tables

* **orders** → transaction-level data
* **products** → product attributes
* **account** → account-related information

---

## 🚀 Author

komal
