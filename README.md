# 🛍️ Customer Loyalty Analysis using RFM Model in Retail with Python

<img width="1920" height="1080" alt="customer segmentation strategy" src="https://github.com/user-attachments/assets/d5d663a7-1945-4a4e-8dee-f3935d08a30b" />


**Author**: Nguyen Anh Huy  
**Date**: 18/05/2025  
**Tools Used**: Python (Jupyter Notebook)

---

## 📚 Table of Contents  
- [I. Background & Overview](#i-background--overview)  
- [II. Dataset Description & Data Structure](#ii-dataset-description--data-structure)  
- [III. Main Process](#iii-main-process)  
  - [EDA (Exploratory Data Analysis)](#eda-exploratory-data-analysis)  
  - [Data Processing & RFM Calculation](#data-processing--rfm-calculation)  
  - [Visualization & Customer Segmentation](#visualization--customer-segmentation)  
- [IV. Final Conclusion & Recommendations](#iv-final-conclusion--recommendations)

---
## 📌 I. Background & Overview

### 📖 What is this project about?

The **Marketing team** of a retail company aims to launch personalized customer campaigns for the holiday season, including both **retention** and **acquisition** strategies. Due to the large volume of transactional data, traditional manual segmentation is no longer viable.  

To address this, the **RFM model** is implemented using Python to analyze purchasing behavior and segment customers based on **Recency**, **Frequency**, and **Monetary** metrics.  

This project covers the entire analytical flow:  
✔️ Data cleaning & preparation  
✔️ RFM score computation  
✔️ Customer segmentation  
✔️ Visualization  
✔️ Business recommendations  

### 👤 Who is this project for?

✔️ Marketing & Sales Department  
✔️ Business stakeholders & decision-makers  

---

### ❓ Business Questions

- How can we segment our customers effectively using the RFM framework?  
- Which segments should be prioritized for retention or promotion campaigns?  
- What customer insights can be extracted to enhance marketing performance?  
- What strategies should be applied to different customer tiers to maximize lifetime value?

---

### 📊 Why use the RFM Model?

**RFM (Recency, Frequency, Monetary)** is a proven method to understand customer purchasing behavior:

- **Recency**: How recently did the customer make a purchase?  
- **Frequency**: How often do they purchase?  
- **Monetary**: How much have they spent?

By applying RFM analysis, companies can:
- Identify loyal, at-risk, and high-value customers
- Tailor communication strategies for each segment
- Optimize promotional spending and campaign effectiveness

---

## 📂 II. Dataset Description & Data Structure

### 📌 Data Source

- **Source**: Internal e-commerce retail dataset  
- **Format**: Excel workbook (`.xlsx`)  
- **Size**: 541,910 rows × 8 columns across 2 sheets  

---

### 📁 Data Structure & Relationships

#### 1️⃣ Tables Used

- **Sheet 1: E-commerce Retail** – Transaction-level data (orders, quantities, timestamps, customer IDs, pricing).  
- **Sheet 2: Segmentation** – RFM scores and segmentation results per customer.

---

<details>
<summary>📋 <strong>Dataset Schema: Sheet 1 - E-commerce Retail</strong></summary>

| Column       | Data Type | Description |
|--------------|------------|-------------|
| InvoiceNo    | OBJECT     | Invoice number (starts with 'C' if canceled) |
| StockCode    | OBJECT     | Product/item code |
| Description  | OBJECT     | Product name |
| Quantity     | INTEGER    | Quantity of product purchased |
| InvoiceDate  | DATETIME   | Date and time of transaction |
| UnitPrice    | FLOAT      | Price per unit |
| CustomerID   | FLOAT      | Unique customer identifier |
| Country      | OBJECT     | Customer’s country |

</details>

<details>
<summary>📊 <strong>RFM Segmentation Mapping: Sheet 2 - Segmentation</strong></summary>

This sheet includes pre-computed or output RFM scores and assigned segments.

| Column      | Description |
|-------------|-------------|
| CustomerID  | Unique customer identifier |
| Recency     | Days since last purchase |
| Frequency   | Number of purchases |
| Monetary    | Total money spent |
| RFM_Score   | Combined RFM score |
| Segment     | Assigned segment (e.g., Champions, At Risk, Hibernating) |

</details>

---


## III. ⚒️ Main Process

---

### 🔍 EDA (Exploratory Data Analysis)

📌 **EDA Goals**:
- Identify and handle missing values, duplicates, and incorrect data types.
- Clean invalid values (e.g., canceled orders, negative quantities).

#### ✅ Key EDA Tasks

| Task                | Action                                                                 |
|---------------------|------------------------------------------------------------------------|
| Convert Data Types  | Convert `InvoiceDate` to datetime, ensure `CustomerID` is formatted    |
| Remove Invalid Rows | Remove rows where Quantity ≤ 0, UnitPrice ≤ 0, or canceled InvoiceNo   |
| Handle Missing Data | Remove rows with missing CustomerID                                    |
| Remove Duplicates   | Drop duplicated rows                                                    |

---

### 🧮 Data Processing & RFM Calculation

📌 **Goal**: Calculate RFM scores and segment customers

#### ✅ Steps
1. **Define Reference Date**: Set as one day after the latest transaction.
2. **Calculate RFM Metrics**:
   - `Recency`: Days since last purchase.
   - `Frequency`: Total number of transactions.
   - `Monetary`: Total spending.
3. **Score Each RFM Metric**: Rank each customer (e.g., score 1–5).
4. **Create RFM Segments**: Combine R, F, M scores for final segmentation.

---

### 📊 Visualization & Customer Segmentation

📌 **Goal**: Visualize key customer segments based on RFM scores.

- Display customer counts per segment
- Highlight high-value customer profiles
- Visualize Recency, Frequency, and Monetary distributions

---

## IV. 🧠 Final Conclusion & Recommendations

### 📝 Insights


### 📌 Recommendations


---


