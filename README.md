# Zepto Inventory Analysis (SQL)

A SQL project that explores, cleans, and analyzes product inventory data from Zepto, a quick-commerce grocery platform. It answers practical business questions about pricing, discounts, stock availability, estimated revenue, and inventory weight.

## Repository Contents

| File | Description |
|------|-------------|
| `zepto_v2.csv` | Raw dataset (3,732 products, 9 columns) |
| `Zepto_SQL_1.sql` | Table creation, data exploration, cleaning, and 8 analysis queries |

## Dataset

Each row is one product (SKU) listing.

| Column | Description |
|--------|-------------|
| category | Product category (14 categories, such as Fruits & Vegetables, Beverages, Munchies, Personal Care) |
| name | Product name |
| mrp | Maximum retail price, stored in **paise** in the raw file |
| discountPercent | Discount offered on MRP |
| availableQuantity | Units available in stock |
| discountedSellingPrice | Selling price after discount, also in **paise** |
| weightInGms | Product weight in grams |
| outOfStock | Whether the product is out of stock (TRUE/FALSE) |
| quantity | Number of units per pack |

Notes on the raw data:
- There are no null values.
- 453 products are marked out of stock.
- Many product names repeat (the same product is listed in multiple pack sizes or variants).
- At least one product has an MRP of 0, which is removed during cleaning.

## Project Steps

### 1. Setup
Creates the `zepto` table with appropriate types (`NUMERIC` for prices, `INTEGER` for quantities, `BOOLEAN` for stock status). Load `zepto_v2.csv` into it using your database's import tool (for example pgAdmin's Import/Export, or `COPY`).

### 2. Data Exploration
- Row count and a sample of the data
- Null value check across all columns
- List of distinct product categories
- In-stock vs. out-of-stock product count
- Product names that appear multiple times

### 3. Data Cleaning
- Find and delete products with price = 0
- Convert `mrp` and `discountedSellingPrice` from paise to rupees (divide by 100)

### 4. Business Analysis

| # | Question |
|---|----------|
| Q1 | Top 10 best-value products by discount percentage |
| Q2 | High-MRP products (above ₹300) that are out of stock |
| Q3 | Estimated revenue for each category |
| Q4 | Products with MRP above ₹500 and discount below 10% |
| Q5 | Top 5 categories with the highest average discount |
| Q6 | Price per gram for products of 100g or more, sorted by best value |
| Q7 | Group products by weight into Low, Medium, and Bulk |
| Q8 | Total inventory weight per category |

Techniques used: aggregation, `GROUP BY` / `HAVING`, `DISTINCT`, `CASE WHEN`, calculated columns, `ROUND`, and filtering with `ORDER BY` / `LIMIT`.

## Tech Stack

- **Database:** PostgreSQL
- **Tools:** pgAdmin / DBeaver / psql

## How to Run

1. Create a PostgreSQL database.
2. Run the `CREATE TABLE` statement from `Zepto_SQL_1.sql`.
3. Import `zepto_v2.csv` into the `zepto` table (CSV with header, UTF-8).
4. Run the exploration, cleaning, and analysis sections in order.
