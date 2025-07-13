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

This section outlines the full analytical flow from data exploration to RFM modeling and customer segmentation.

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

#### 1️⃣ Inspect Data Structure & Data Types

```python
ecommerce_retail.info()
```

<img width="640" height="285" alt="image" src="https://github.com/user-attachments/assets/a01dc65c-18d4-46f1-808b-2aba28a6e40f" />

✅ Insight: Most columns have correct data types. However, CustomerID contains missing values.

#### 2️⃣ Remove Invalid Transactions

We filter out transactions where Quantity or UnitPrice is less than or equal to 0, typically representing canceled or erroneous records.

```python
ecommerce_retail.describe()
```
<img width="686" height="299" alt="image" src="https://github.com/user-attachments/assets/d23dc704-cd76-40eb-becd-cbab09d7b642" />

```python
ecommerce_retail = ecommerce_retail[(ecommerce_retail['UnitPrice'] > 0) & (ecommerce_retail['Quantity'] > 0)]
```
<img width="893" height="635" alt="image" src="https://github.com/user-attachments/assets/6a7871fe-c280-42a8-8ad4-fa65c7a25cef" />

```python
ecommerce_retail = ecommerce_retail[(ecommerce_retail['UnitPrice'] > 0) & (ecommerce_retail['Quantity'] > 0)]
ecommerce_retail.describe()
```
<img width="701" height="308" alt="image" src="https://github.com/user-attachments/assets/942f174a-f1ea-4bc4-ad92-541ca8de162f" />

#### 3️⃣ Handle Missing Data
We identify missing values, especially in the CustomerID column.
```python
missing_dict = {'volume': ecommerce_retail.isnull().sum(), 'missing_rate': ecommerce_retail.isnull().sum()/ecommerce_retail.shape[0]}
missing_df = pd.DataFrame(missing_dict)
missing_df
```
<img width="388" height="306" alt="image" src="https://github.com/user-attachments/assets/40aa9c1c-3074-4318-91db-6fe9bbbce63a" />

✅ Insight: Over 20% of records lack CustomerID, making them unsuitable for customer-level analysis.

🔧 Action: Remove all rows with null values.

```python
ecommerce_retail.dropna(inplace=True)
ecommerce_retail.isnull().sum()
```
<img width="218" height="334" alt="image" src="https://github.com/user-attachments/assets/66bae630-eead-422b-acb1-f72ae60b08a4" />

#### 4️⃣ Remove Duplicate Records
We check for duplicates based on invoice, product, date, and customer:
```python
df_duplication = ecommerce_retail.duplicated(subset=["InvoiceNo", "StockCode", "InvoiceDate", "CustomerID"])
print(ecommerce_retail[df_duplication].shape)
print(ecommerce_retail.shape)
```
<img width="177" height="56" alt="image" src="https://github.com/user-attachments/assets/8859ac3f-c500-41a8-81bc-b0e2f48c6f2f" />

```python
ecommerce_retail.drop_duplicates(subset=["InvoiceNo","StockCode","InvoiceDate","CustomerID"], inplace=True)
ecommerce_retail.shape
```
<img width="151" height="39" alt="image" src="https://github.com/user-attachments/assets/d4c4d65f-9524-4d91-8ca4-0987a0753c91" />

✅ Dataset size reduced to ~388K rows after cleaning.

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

#### 1️⃣ Define Reference Date & Calculate RFM Metrics
```python
# define total price
ecommerce_retail['TotalPrice'] = ecommerce_retail['UnitPrice']*ecommerce_retail['Quantity']

# define last day
last_day = ecommerce_retail['InvoiceDate'].max()

# RFM
RFM_df = ecommerce_retail.groupby('CustomerID').agg(
    Recency = ('InvoiceDate', lambda x: last_day - x.max()),
    Frequency = ('CustomerID', 'count'),
    Monetary = ('TotalPrice','sum'),
    Start_Day = ('InvoiceDate', 'min')
).reset_index()

RFM_df['Recency'] = RFM_df['Recency'].dt.days.astype('int')
RFM_df['Recency_reverse'] = - RFM_df['Recency']
RFM_df['Start_Day'] = pd.to_datetime(RFM_df['Start_Day'])
RFM_df['Start_Month'] = RFM_df['Start_Day'].apply(lambda x: x.strftime('%Y-%m'))
RFM_df.head()
```
<img width="803" height="203" alt="image" src="https://github.com/user-attachments/assets/e0baa6c0-8c2d-46b7-a06d-cc6658b70df2" />

#### 2️⃣ Score Each RFM Metric
We use qcut to divide each metric into 5 groups and combine them into an RFM score.
```python
# Using qcut to create R, F, M
RFM_df['R'] = pd.qcut(RFM_df['Recency_reverse'], 5, labels=[1, 2, 3, 4, 5]).astype(str)
RFM_df['F'] = pd.qcut(RFM_df['Frequency'], 5, labels=[1, 2, 3, 4, 5]).astype(str)
RFM_df['M'] = pd.qcut(RFM_df['Monetary'], 5, labels=[1, 2, 3, 4, 5]).astype(str)
RFM_df['RFM'] = RFM_df.apply(lambda x: x['R'] + x['F'] + x['M'], axis=1)
RFM_df.head()
```
<img width="881" height="200" alt="image" src="https://github.com/user-attachments/assets/4459b9b8-8173-43e7-9290-07a75717b110" />

#### 3️⃣ Create RFM Segments
We use a predefined segmentation mapping from a second sheet.
```python
# Segmentation
Segmentation = pd.read_excel('ecommerce retail.xlsx', sheet_name="Segmentation")
Segmentation['RFM Score'] = Segmentation['RFM Score'].str.split(',')
Segmentation = Segmentation.explode('RFM Score').reset_index(drop=True)
Segmentation.head()
```
Then merge with our main RFM table:
```python
Segmentation['RFM Score'] = Segmentation['RFM Score'].apply(lambda x: x.strip())
RFM_df_final = RFM_df.merge(Segmentation, left_on='RFM', right_on='RFM Score', how='left')
RFM_df_final.head()
```
<img width="1126" height="215" alt="image" src="https://github.com/user-attachments/assets/ff70516d-c9f0-4707-8449-36d3b46d3258" />

📌 At this stage, we have a complete customer-level segmentation table ready for visualization and strategic analysis.

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


