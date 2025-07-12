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

## I. 📖 Background & Overview

### 🎯 Context  
SuperStore is a global e-commerce company with a large customer base. The Marketing Department wanted to design tailored marketing campaigns for loyal and high-value customers during the holiday season. However, with a large volume of transaction data, manual segmentation was no longer feasible.

The Data Analytics team was tasked with implementing a customer segmentation model using the RFM technique, allowing scalable and strategic customer insights for campaign execution.

### 🔍 What is the RFM Model?  
The **RFM model** is a behavioral segmentation method that scores customers based on:

- **Recency**: How recently a customer made a purchase.  
- **Frequency**: How often the customer made a purchase.  
- **Monetary**: How much the customer spent.

These scores are then used to cluster customers into distinct groups for targeted marketing.

### ✅ Objectives  
✔️ Segment customers based on RFM scores to enable data-driven marketing strategies.  
✔️ Identify which RFM metric is most impactful in retail segmentation.  

👤 **Who is this project for?**  
- Data Analysts & Business Analysts  
- Marketing Directors & Stakeholders  
- E-commerce Managers

---

## II. 📂 Dataset Description & Data Structure

This is a transnational dataset containing all transactions from 01/12/2010 to 09/12/2011 for a UK-based online retail store.

**File**: `ecommerce_retail.xlsx`

<details>
<summary>📄 Dataset Schema</summary>

| Column       | Data Type | Description                                                                 |
|--------------|-----------|-----------------------------------------------------------------------------|
| InvoiceNo    | Object    | Unique invoice number. ‘C’ indicates a cancelled order.                    |
| StockCode    | Object    | Unique product code.                                                        |
| Description  | Object    | Product name.                                                               |
| Quantity     | Integer   | Number of products bought.                                                  |
| InvoiceDate  | Datetime  | Date and time of transaction.                                               |
| UnitPrice    | Float     | Price per product unit.                                                     |
| CustomerID   | Float     | Unique customer ID.                                                         |
| Country      | Object    | Customer’s country of origin.                                               |

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


