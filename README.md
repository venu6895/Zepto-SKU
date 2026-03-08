## Zepto Inventory & Pricing Analysis (SQL Project)

## Project Overview
This project analyzes a Zepto product dataset to understand pricing strategies, discounts, inventory availability, and category performance. The dataset was originally stored in Excel and then imported into a SQL database for analysis.

The goal of this project is to demonstrate data exploration, data cleaning, and business analysis using SQL.

## Dataset Information

The dataset contains product-level information including:

- SKU ID
- Product Name
- Category
- Maximum Retail Price (MRP)
- Discount Percentage
- Discounted Selling Price
- Available Quantity
- Product Weight (grams)
- Stock Availability

This data helps analyze inventory distribution, pricing efficiency, and discount patterns.

## Database Structure

CREATE TABLE zepto (
sku_id SERIAL PRIMARY KEY,
category VARCHAR(120),
name VARCHAR(150) NOT NULL,
mrp NUMERIC(8,2),
discountPercent NUMERIC(5,2),
availableQuantity INTEGER,
discountedSellingPrice NUMERIC(8,2),
weightInGms INTEGER,
outOfStock BOOLEAN,
quantity INTEGER
);

## Project Workflow

### 1. Data Import
- Imported the dataset from Excel into a SQL database.

### 2. Data Exploration
Performed exploratory analysis using SQL queries to understand:
- Total number of records
- Product categories
- Stock availability
- Duplicate product names
- Missing values

Example query:

SELECT COUNT(*) FROM zepto;

### 3. Data Cleaning

Data cleaning steps included:
- Removing products with incorrect pricing
- Identifying missing values
- Converting price values from paise to rupees

Example transformation:

UPDATE zepto
SET mrp = mrp / 100.0,
discountedSellingPrice = discountedSellingPrice / 100.0;

## Data Analysis

Several SQL queries were used to generate business insights.

### Top Discounted Products

SELECT name, mrp, discountPercent
FROM zepto
ORDER BY discountPercent DESC
LIMIT 10;

### High MRP Products Out of Stock

SELECT name, mrp
FROM zepto
WHERE outOfStock = TRUE AND mrp > 300;

### Category Revenue Analysis

SELECT category,
SUM(discountedSellingPrice * availableQuantity) AS total_revenue
FROM zepto
GROUP BY category;

### Product Value Analysis (Price per Gram)

SELECT name, weightInGms,
discountedSellingPrice / weightInGms AS price_per_gram
FROM zepto;

## Key Insights

- Identified products with the highest discounts
- Found high-value products that are out of stock
- Calculated category-wise revenue potential
- Determined best-value products using price-per-gram analysis

## Tools Used

- SQL (MySQL / PostgreSQL)
- Excel
- Data Cleaning
- Data Analysis
  
## Skills Demonstrated

- SQL Querying
- Data Cleaning
- Data Exploration
- Business Data Analysis
- Inventory & Pricing Analysis

## Future Improvements

- Build a Power BI dashboard using the dataset
- Automate analysis using Python
- Create a data pipeline for inventory tracking
