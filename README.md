# RetailMart Sales Data Pipeline

## 📌 Project Overview

RetailMart Pvt. Ltd. is a retail company operating stores across India. The company collects daily sales data from multiple stores in the form of CSV files.

The raw data may contain common real-world data quality issues such as:

* Missing values
* Duplicate records
* Incorrect data types
* Inconsistent or incomplete information

The objective of this project is to build a small **ETL (Extract, Transform, Load) data pipeline** that cleans, transforms, combines, and loads the data into a SQLite database for further analysis and reporting.

The complete pipeline has been implemented using **Python and Jupyter Notebook**.

---

## 🎯 Project Objectives

The main objectives of this project are:

* Load data from multiple CSV files
* Inspect the structure and quality of the data
* Identify missing values
* Remove duplicate records
* Handle missing and invalid data
* Convert columns to appropriate data types
* Merge data from different sources
* Calculate total revenue
* Perform business-level analysis
* Store the processed data in a SQLite database
* Execute SQL queries for reporting
* Generate useful business insights
* Implement the complete workflow as a reusable pipeline
* Handle missing input files using basic error handling

---

## 📂 Project Structure

```text
RetailMart-Sales-Data-Pipeline/
│
├── sales_data.csv
├── products.csv
├── stores.csv
├── RetailMart_Sales_Pipeline.ipynb
└── README.md
```

---

## 📊 Dataset Description

This project uses three different CSV files as data sources.

### 1. `sales_data.csv`

Contains daily sales transaction information.

| Column       | Description                     |
| ------------ | ------------------------------- |
| `sale_id`    | Unique identifier for each sale |
| `store_id`   | Identifier of the store         |
| `product_id` | Identifier of the product       |
| `quantity`   | Number of units sold            |
| `sale_date`  | Date on which the sale occurred |
| `amount`     | Sales amount                    |

The sales dataset intentionally contains some data quality issues to simulate real-world scenarios.

These include:

* Missing values in `quantity`
* Missing values in `amount`
* Duplicate records

---

### 2. `products.csv`

Contains information about the products sold by RetailMart.

| Column         | Description                      |
| -------------- | -------------------------------- |
| `product_id`   | Unique identifier of the product |
| `product_name` | Name of the product              |
| `category`     | Category of the product          |
| `price`        | Price of the product             |

---

### 3. `stores.csv`

Contains information about RetailMart stores.

| Column       | Description                       |
| ------------ | --------------------------------- |
| `store_id`   | Unique identifier of the store    |
| `store_name` | Name of the store                 |
| `city`       | City where the store is located   |
| `region`     | Region where the store is located |

---

# 🔄 ETL Pipeline

The project follows a basic ETL workflow:

```text
Raw CSV Files
      ↓
Data Ingestion
      ↓
Data Cleaning
      ↓
Data Transformation
      ↓
Data Analysis
      ↓
SQLite Database
      ↓
SQL Reporting
      ↓
Business Insights
```

---

# 📥 Task 1: Data Ingestion

The first stage of the pipeline is to load all three CSV files into Pandas DataFrames.

The following activities are performed:

* Load `sales_data.csv`
* Load `products.csv`
* Load `stores.csv`
* Check the shape of each DataFrame
* Display the first five rows
* Check for missing values
* Generate a summary of null values in each column

### Questions Addressed

* What is the structure of each dataset?
* How many rows and columns are present?
* Which columns contain missing values?
* What type of data is present in each source?

---

# 🧹 Task 2: Data Cleaning

The raw sales data contains duplicate and missing records. The data cleaning stage prepares the dataset for further processing.

### Cleaning Operations

* Identify duplicate rows
* Remove duplicate records
* Count the number of duplicates found
* Replace missing values in `quantity` with `0`
* Remove records where `amount` is missing
* Convert `sale_date` into the appropriate datetime format
* Convert `amount` into a floating-point data type
* Check the shape of the cleaned dataset

### Questions Addressed

* How many duplicate records are present?
* How many records remain after removing duplicates?
* Which columns contain missing values?
* How should missing quantities be handled?
* Which records should be removed because of missing values?
* Are the date and amount columns stored in the correct format?

---

# 🔗 Task 3: Data Transformation

After cleaning the data, the datasets are combined to create a single analysis-ready dataset.

The sales data is merged with:

* Product information using `product_id`
* Store information using `store_id`

This provides a complete view of each transaction, including:

* Product name
* Product category
* Product price
* Store name
* City
* Region
* Quantity sold
* Sale date

---

## 💰 Revenue Calculation

A new column named `total_revenue` is created using:

**Total Revenue = Quantity × Product Price**

NumPy is then used to calculate:

* Mean total revenue
* Maximum total revenue
* Minimum total revenue

---

## 🏙️ Revenue by City

The data is grouped by city to calculate the total revenue generated by each city.

The result is sorted in descending order to identify the highest-performing cities.

### Business Question

> Which city generates the highest total revenue?

---

# 🗄️ Task 4: Data Loading

After cleaning and transformation, the final dataset is loaded into a **SQLite database**.

The final data is stored in a table named:

`retail_sales`

This allows the cleaned data to be queried using SQL.

---

# 🔍 SQL Analysis

## Top 3 Best-Selling Products

A SQL query is used to identify the **Top 3 best-selling products** based on the total quantity sold.

### Business Question

> Which three products have the highest total quantity sold?

---

## 💵 Total Revenue Per Store Per Day

A SQL query is used to calculate the total revenue generated by each store on each day.

### Business Question

> How much revenue does each store generate per day?

This helps compare the daily performance of different stores.

---

# 📈 Task 5: Reporting & Insights

A summary report is generated using Python.

The report contains the following information:

### Total Number of Transactions

The total number of valid transactions available after data cleaning.

### Total Revenue

The overall revenue generated from the cleaned and transformed dataset.

### Top-Selling City

The city generating the highest total revenue.

### Top-Selling Product

The product with the highest total quantity sold.

---

# ⚙️ Task 6: Pipeline & Error Handling

The complete workflow is combined into a single function called:

`run_pipeline()`

The function executes the complete process:

```text
Load
 ↓
Clean
 ↓
Transform
 ↓
Analyze
 ↓
Load to Database
 ↓
Generate Report
```

Basic error handling is also implemented.

If any required CSV file is missing, the pipeline displays an appropriate error message instead of terminating unexpectedly.

---

# 🛠️ Technologies Used

| Technology           | Purpose                                               |
| -------------------- | ----------------------------------------------------- |
| **Python**           | Pipeline development                                  |
| **Pandas**           | Data ingestion, cleaning, transformation and analysis |
| **NumPy**            | Numerical calculations                                |
| **SQLite**           | Database storage                                      |
| **SQL**              | Data analysis and reporting                           |
| **Jupyter Notebook** | Development and execution                             |
| **Git & GitHub**     | Version control and project documentation             |

---

# 📋 Key Business Questions

This project answers the following business questions:

1. Which products are selling the most?
2. Which city generates the highest revenue?
3. What is the total revenue generated by each city?
4. What are the Top 3 best-selling products?
5. What is the total revenue generated by each store per day?
6. What is the total number of valid transactions?
7. What is the overall revenue generated?
8. Which product is the top-selling product?
9. Which stores or products contain missing information?
10. How can raw retail data be transformed into a clean, analysis-ready dataset?

---

# 📊 Data Quality Checks

The pipeline performs several data quality checks, including:

* Missing value detection
* Duplicate record detection
* Data type validation
* Missing sales amount handling
* Missing quantity handling
* Date format conversion
* Final merged dataset validation

These checks help ensure that the data is reliable before it is used for reporting.

---

# 🎓 Key Learning Outcomes

Through this project, I gained practical experience in:

* Building an ETL pipeline
* Working with multiple CSV data sources
* Data ingestion using Pandas
* Data cleaning and preprocessing
* Handling missing values
* Removing duplicate records
* Data type conversion
* Joining multiple datasets
* Creating calculated columns
* Using NumPy for numerical analysis
* Performing GroupBy operations
* Working with SQLite databases
* Writing SQL analytical queries
* Generating business reports
* Implementing reusable Python pipelines
* Adding basic error handling
* Documenting a data engineering project

---

# 🚀 How to Run the Project

## Prerequisites

Make sure the following are installed:

* Python
* Jupyter Notebook
* Pandas
* NumPy

SQLite is used for database operations.

# 📌 Project Highlights

* Built an end-to-end retail data pipeline
* Worked with multiple raw CSV data sources
* Simulated real-world data quality issues
* Cleaned and transformed raw sales data
* Combined sales, product, and store datasets
* Calculated revenue metrics
* Performed city-level sales analysis
* Stored processed data in SQLite
* Used SQL for business reporting
* Created a reusable pipeline function
* Implemented basic error handling

---

# ⭐ Conclusion

This project demonstrates a complete data processing workflow starting from raw CSV files and ending with a clean, structured, and analysis-ready dataset.

It provides practical experience with the core concepts of **Data Engineering, ETL, Data Cleaning, Data Transformation, SQL, Database Loading, and Business Reporting**.

```text
Raw Data
   ↓
Ingestion
   ↓
Cleaning
   ↓
Transformation
   ↓
Analysis
   ↓
Database
   ↓
Reporting
```
