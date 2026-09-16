Dominos POS Data Analysis & Customer Segmentation
This repository contains an end-to-end data pipeline for analyzing Domino's Pizza Point of Sale (POS) transactions, spanning raw data engineering to machine-learning-driven customer segmentation.

1. Data Access & Preparation
Export to CSV: All tables from the relational database (SSMS) were exported to CSV format to ensure fast, reproducible data access without requiring a direct database connection.
Data Joining: The Orders table (transaction header details) and Order_Lines table (line-item details) were joined using Location_Code, Order_Number, and Order_Date composite keys.

2. Analysis Workflow
Data Cleaning & Filtering:
Removed special control characters (\r\n) and extraneous whitespace across string fields.
Filtered out zero/negative quantity values and price anomalies.
Stripped administrative non-food line items (delivery fees, plastic bags, condiment sachets) to focus strictly on core menu sales.
Exploratory Data Analysis (EDA):
Identified sales temporal trends, peak operating hours (lunch and late afternoon surges), and top-selling menu items.
Evaluated discount sensitivity and full-price transaction ratios.
Market Basket Analysis:
Applied itertools.combinations to uncover frequent item pairings and bundle candidates (such as single-serve chicken meals with beverages).
Customer Segmentation (Unsupervised Machine Learning):
RFM Aggregation: Engineered Recency (days since last purchase), Frequency (total transactions), and Monetary (total items purchased) metrics per customer relative to December 31, 2025.
Outlier Removal & Scaling: Removed internal system/dummy accounts (Frequency > 300) and applied StandardScaler to normalize feature distributions.
K-Means Clustering: Segmented customers into 3 core groups (Active Regulars, At-Risk / Lapsed, and VIP Power Users).

3. Business Results & CRM Integration
The final K-Means segmentation output has been exported to segmented_customers_2025.csv, providing clean cluster labels ready for integration with marketing automation platforms (such as targeted WhatsApp or email campaigns).