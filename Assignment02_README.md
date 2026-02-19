# **Big Data Assignment 02 – End-to-End Data Pipeline (PySpark \+ MongoDB)**

# **Assignment Overview**

This project implements a complete data engineering pipeline using PySpark and mongoDB based on the given dataset (**Kaggle – E-Commerce Data (Online Retail Transactions)**UK-based online retail transactional dataset (2010–2011))

Assignment implements a complete big data pipeline using the Medallion Architecture:

* Bronze Layer (Raw Data)  
* Silver Layer (Cleaned Data)  
* Gold Layer (Analytics & Data Warehouse)  
* MongoDB Integration  
* Bonus Component (Advanced Analytics)

The pipeline is designed to run in a **Run-All safe mode** without restarting the runtime.

# **Tools & Technologies Used**

* Python  
* PySpark  
* Apache Spark  
* MongoDB Atlas  
* Google Colab  
* Google Drive (Storage)  
* Parquet File Format

# **Project Architecture (Medallion Design)**

Raw CSV Data → Bronze Layer → Silver Layer → Gold Layer → MongoDB  
**Task 1 – Environment Setup & Library Installation**

### **What We Did:**

* Mounted Google Drive  
* Installed required libraries  
* Created Spark session  
* Configured MongoDB connection (optional at later stage)

### **Purpose:**

This step prepares the environment to process big data using PySpark in Google Colab.

Key Setup Includes:

* pyspark installation  
* pymongo installation  
* Secure Mongo URI using Colab secrets

**Important :** 

**Steps to add Secure secrets in colab:**

In this screenshot you can see icon like key and click that icon, after that it contains option like add secret using this option can store MongoDB URI like a secret and when try to code no more visible code using Mongo URI. so its may affect to security also because the MongoDB string shows all the data can connect to Database.

# 

# **Task 2 – Data Ingestion (Loading Dataset)**

### **What We Did:**

* Loaded the e-commerce dataset (CSV)  
* Converted it into a Spark DataFrame  
* Checked schema and previewed data

### **Purpose:**

To ingest raw data into Spark for distributed processing.

Output:

* Raw DataFrame (Bronze\_df initial stage)  
* In drive path created Data Quality Report (.csv file)

# **Task 3 – Bronze Layer (Raw Data Storage)**

### **What We Did:**

* Stored raw data into Bronze layer  
* Partitioned by year and month  
* Saved as Parquet format in Google Drive

### **Purpose:**

The Bronze layer stores original, uncleaned data for traceability and backup.

Features:

* Immutable raw data  
* Partitioned storage for performance  
* No heavy transformations

Output Path Example:

**/drive/MyDrive/BigData\_Assignment02/bronze/**

# **Task 4 – Silver Layer (Data Cleaning & Transformation)**

### **What We Did:**

* Removed null CustomerID values  
* Fixed data types  
* Cleaned invalid records  
* Standardized columns

### **Purpose:**

The Silver layer contains clean and structured data ready for analytics.

Transformations Performed:

* Null handling  
* Data filtering  
* Schema correction  
* Feature engineering (year, month columns)

Output:

Silver Data (Cleaned Dataset)

# **Task 5 – Gold Layer (Data Warehouse Tables)**

### **What We Did:**

Created dimensional model tables:

* Fact Table: `fact_invoices`  
* Dimension Table: `dim_customers`  
* Dimension Table: `dim_products`

### **Purpose:**

To support business analytics and BI queries using a star schema design.

Benefits:

* Faster querying  
* Structured analytics  
* Scalable data warehouse design

# **Task 6 – MongoDB Integration (Data Export)**

### **What We Did:**

* Connected Spark to MongoDB Atlas  
* Exported Gold Layer tables into MongoDB collections  
* Used Mongo Spark Connector

Collections Created:

* fact\_invoices  
* dim\_customers  
* dim\_products

### **Important Note:**

Spark session was recreated with MongoDB connector to avoid:

DATA\_SOURCE\_NOT\_FOUND: mongodb

# **Task 7 – Run-All Safe Execution (Without Restart Runtime)**

### **Problem Faced:**

Spark and MongoDB connector errors when running all cells without restarting runtime.

### **Solution Implemented:**

* Forced Spark stop  
* Cleared active Spark session  
* Recreated Spark with Mongo connector

This ensures:

* Stable execution  
* No runtime restart required  
* Reproducible notebook

# **Bonus Component Implemented**

## **Frequent Item Pair Analysis (Market Basket Analysis)**

### **What We Did:**

* Grouped products per invoice  
* Generated item pairs  
* Calculated frequency of item combinations

### **Purpose:**

To identify frequently purchased product pairs for business insights and recommendation systems.

Example Insight:  
Customers who buy Item A often buy Item B.

# 

# **Data Storage Structure**

BigData\_Assignment02/  
│  
├── bronze/     (Raw Parquet Data)  
├── silver/     (Cleaned Data)  
├── gold/       (Fact & Dimension Tables)  
└── notebook.ipynb

# **Requirements to Run This Project**

Before starting, install:

\!pip install pyspark         (Colab Required “\!” with install pip)  
\!pip install pymongo  
\!pip install dnspython

Google Colab Requirements:

* Google Drive Access  
* MongoDB URI stored in Colab Secrets  
* Stable internet connection

# **Challenges Faced & Solutions**

| Issue | Solution |
| ----- | ----- |
| Spark overwrite parquet error | Cleared output directory manually |
| MongoDB connector not found | Recreated Spark with connector package |
| Runtime restart problem | Used Spark session reset method |
| Missing CustomerID records | Filtered null values in Silver layer |

# **Key Learning Outcomes**

* End-to-end Big Data pipeline design  
* Medallion Architecture implementation  
* PySpark data processing at scale  
* MongoDB integration with Spark  
* Error handling in distributed systems  
* Run-All safe notebook development

# **Conclusion**

This assignment successfully demonstrates a scalable big data processing pipeline using PySpark and MongoDB.  
The system follows industry best practices such as:

* Layered architecture (Bronze, Silver, Gold)  
* Clean ETL workflow  
* Distributed data processing  
* Cloud-based storage and execution

The final solution is optimized to run in Google Colab without requiring runtime restarts, making it stable, reproducible, and suitable for academic evaluation.

