# 🛒 Zepto E-commerce SQL Data Analyst Portfolio Project

A real-world data analyst portfolio project using an e-commerce inventory dataset scraped from Zepto, one of India’s fastest-growing quick-commerce startups. It covers the full analyst workflow from raw data exploration to business-focused insights.

## 📌 Project Overview

The goal is to simulate how actual data analysts in the e-commerce or retail industries work behind the scenes to use SQL to:

✅ Set up a messy, real-world e-commerce inventory **database**  

✅ Perform **Exploratory Data Analysis (EDA)** to explore product categories, availability, and pricing inconsistencies  

✅ Implement **Data Cleaning** to handle null values, remove invalid entries, and convert pricing from paise to rupees  

✅ Write **business-driven SQL queries** to derive insights around **pricing, inventory, stock availability, revenue** and more  

## 📁 Dataset Overview

The dataset was sourced from [Kaggle](https://www.kaggle.com/datasets/palvinder2006/zepto-inventory-dataset/data?select=zepto_v2.csv) and was originally scraped from Zepto’s official product listings. It mimics what you’d typically encounter in a real-world e-commerce inventory system.

Each row represents a unique SKU (Stock Keeping Unit) for a product. Duplicate product names exist because the same product may appear multiple times in different package sizes, weights, discounts, or categories to improve visibility – exactly how real catalog data looks.

🧾 **Columns:**

- **sku_id:** Unique identifier for each product entry (Synthetic Primary Key)  
- **name:** Product name as it appears on the app  
- **category:** Product category like Fruits, Snacks, Beverages, etc.  
- **mrp:** Maximum Retail Price (originally in paise, converted to ₹)  
- **discountPercent:** Discount applied on MRP  
- **discountedSellingPrice:** Final price after discount (also converted to ₹)  
- **availableQuantity:** Units available in inventory  
- **weightInGms:** Product weight in grams  
- **outOfStock:** Boolean flag indicating stock availability  
- **quantity:** Number of units per package (mixed with grams for loose produce)  

## 🔧 Project Workflow

Here’s a step-by-step breakdown of what we do in this project:

### 1. Database & Table Creation

We start by creating a SQL table with appropriate data types:

```sql
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
2. Data Import
Loaded CSV using pgAdmin's import feature.

If you're not able to use the import feature, write this code instead:

sql
Copy code
\copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv'
WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');
Faced encoding issues (UTF-8 error), which were fixed by saving the CSV file using CSV UTF-8 format.

3. 🔍 Data Exploration
Counted the total number of records in the dataset

Viewed a sample of the dataset to understand structure and content

Checked for null values across all columns

Identified distinct product categories available in the dataset

Compared in-stock vs out-of-stock product counts

Detected products present multiple times, representing different SKUs

4. 🧹 Data Cleaning
Identified and removed rows where MRP or discounted selling price was zero

Converted mrp and discountedSellingPrice from paise to rupees for consistency and readability

📊 Business Insights & Visualizations
All charts are generated from SQL outputs using Python/Matplotlib and stored in the charts/ folder.

1️⃣ Top 10 Best-Value Products (Highest Discount %)
SQL: Top 10 SKUs ordered by discountPercent (descending) to identify best-value deals for customers.


2️⃣ High-MRP Products That Are Out of Stock
SQL: Filtered products where outOfStock = TRUE and mrp > 300 to highlight high-value stockouts.


3️⃣ Estimated Revenue per Category
SQL: SUM(discountedSellingPrice * availableQuantity) grouped by category to estimate potential revenue.


4️⃣ Expensive Products with Low Discounts
SQL: Filter where mrp > 500 and discountPercent < 10 to find premium products that are not heavily discounted.


5️⃣ Top 5 Categories by Average Discount
SQL: AVG(discountPercent) grouped by category and sorted to identify most discounted categories.


6️⃣ Price per Gram – Value-for-Money Analysis
SQL: Compute discountedSellingPrice / weightInGms for products with weightInGms >= 100 to compare value across SKUs.


7️⃣ Product Weight Segmentation (Low / Medium / Bulk)
SQL: Categorized products using a CASE expression on weightInGms into Low, Medium, and Bulk.


8️⃣ Total Inventory Weight per Category
SQL: SUM(weightInGms * availableQuantity) grouped by category to understand physical inventory load.


💡 Thanks for checking out the project!











