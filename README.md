# 🛍️ Customer Loyalty Analysis using RFM Model in Retail with Python

<img width="1920" height="1080" alt="customer segmentation strategy" src="https://github.com/user-attachments/assets/d5d663a7-1945-4a4e-8dee-f3935d08a30b" />


**Author**: Nguyen Anh Huy  
**Date**: 18/05/2025  
**Tools Used**: Python (Jupyter Notebook)

---

## 📚 Table of Contents  
- [📌 I. Background & Overview](https://github.com/yuhanguyen1/Customer-loyalty-analysis-based-on-RFM-model-in-Retail-Using-Python?tab=readme-ov-file#-i-background--overview)  
- [📂 II. Dataset Description & Data Structure](https://github.com/yuhanguyen1/Customer-loyalty-analysis-based-on-RFM-model-in-Retail-Using-Python?tab=readme-ov-file#-ii-dataset-description--data-structure)  
- [⚒️ III. Main Process](https://github.com/yuhanguyen1/Customer-loyalty-analysis-based-on-RFM-model-in-Retail-Using-Python?tab=readme-ov-file#%EF%B8%8F-iii-main-process)  
  - [EDA (Exploratory Data Analysis)](https://github.com/yuhanguyen1/Customer-loyalty-analysis-based-on-RFM-model-in-Retail-Using-Python?tab=readme-ov-file#-eda-exploratory-data-analysis)
  - [Data Processing & RFM Calculation](https://github.com/yuhanguyen1/Customer-loyalty-analysis-based-on-RFM-model-in-Retail-Using-Python?tab=readme-ov-file#-data-processing--rfm-calculation)  
  - [Visualization & Customer Segmentation](https://github.com/yuhanguyen1/Customer-loyalty-analysis-based-on-RFM-model-in-Retail-Using-Python?tab=readme-ov-file#-visualization--customer-segmentation)  
- [🧠 IV. Final Conclusion & Recommendations](https://github.com/yuhanguyen1/Customer-loyalty-analysis-based-on-RFM-model-in-Retail-Using-Python?tab=readme-ov-file#-iv-final-conclusion--recommendations)

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


## ⚒️ III. Main Process

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

### 📊 Data Processing & RFM Calculation  

**🎯 Goal**: Calculate RFM scores and segment customers based on purchasing behavior.  

#### ✅ Steps  

1. **Define Reference Date**  
   - Set the reference date as **one day after the latest transaction** in the dataset.  
   - This ensures accurate calculation of days since the last purchase (Recency).  

2. **Calculate RFM Metrics**  
   - **Recency (R):** Number of days since the customer’s last purchase.  
   - **Frequency (F):** Total number of transactions made by the customer.  
   - **Monetary (M):** Total amount of money spent by the customer.  

3. **Score Each RFM Metric (1–5)**  
   - Each customer is ranked into **five groups (quintiles)** for each metric.  
   - Each RFM metric is divided into **five groups (quintiles)** to ensure a balanced distribution of customers across the scoring scale.  
   - Using 5 levels provides enough granularity to distinguish meaningful differences in customer behavior, while keeping the segmentation simple and interpretable.  
   - A score of **1** always represents the least desirable behavior (e.g., very inactive, very low frequency/spending), while **5** represents the most desirable (e.g., very recent purchase, very frequent, high spender).  


   #### Meaning of Scores:  

   | Metric      | Score = 1 (Lowest)                         | Score = 5 (Highest)                     |
   |-------------|--------------------------------------------|------------------------------------------|
   | **Recency** | Purchased a long time ago (inactive)       | Purchased very recently (highly engaged) |
   | **Frequency** | Very few purchases, low engagement        | Many purchases, very frequent buyer      |
   | **Monetary** | Very low total spending                   | High total spending, valuable customer   |

   👉 In summary: **1 = least valuable behavior, 5 = most valuable behavior**.  

4. **Create RFM Segments**  
   - Combine R, F, and M scores into a **segment code** (e.g., R=5, F=4, M=5 → "545").  
   - These codes are then mapped into intuitive customer groups, such as:  
     - **Champions (555, 554, …):** Recent, frequent, and high-spending customers.  
     - **Potential Loyalists:** Recent buyers with growing frequency and spending.  
     - **At Risk:** Previously valuable but haven’t purchased for a long time.  
     - **Hibernating:** Inactive customers with low frequency and low spending.  


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

### 📍 Part 1: Segment-level Insights for Campaign Strategy

This section provides visualizations to answer key business questions such as:

- **Which customer segments should be prioritized for retention or promotion campaigns?**
- **What customer insights can be extracted to enhance marketing performance?**
- **What strategies should be applied to different customer tiers to maximize lifetime value?**

---

#### 1️⃣ Number of Customers per Segment

<img width="846" height="509" alt="image" src="https://github.com/user-attachments/assets/2867d559-1ae3-4752-a76c-b679c820ff50" />

---

#### 2️⃣ Total Revenue by Segment

<img width="847" height="424" alt="image" src="https://github.com/user-attachments/assets/4d60d5c5-c9c5-4718-8c2f-5bb4bf6502c9" />

---

#### 3️⃣ Average Recency / Frequency / Monetary by Segment

<img width="850" height="479" alt="image" src="https://github.com/user-attachments/assets/b446a6d6-790f-4ef5-ae53-5e216091c40a" />

---

#### 4️⃣ Segments over Time (Cohort by Start Month)

<img width="843" height="446" alt="image" src="https://github.com/user-attachments/assets/4de2dded-0cb3-4d00-bb11-191fa9b847b2" />

---

## 📊 Key Findings

Based on the segment-level analysis of Recency (R), Frequency (F), and Monetary (M), we can draw key behavioral insights for each of the 11 customer segments as follows:

| Segment               | R (Recency)         | F (Frequency)           | M (Monetary)            | Behavioral Insights |
|-----------------------|---------------------|--------------------------|--------------------------|---------------------|
| **Champions (17%)**          | Very recent (~10–20 days)  | Extremely frequent (~200+ purchases) | Highest (~27% of total revenue) | Top-performing customers who purchase often and recently. They are vital to the business and should be consistently rewarded and retained. |
| **Loyal (9%)**              | Moderately recent (~60 days) | High frequency (~180 purchases)     | Considerable (~13% of revenue) | Reliable customers with stable buying habits. Sustained engagement and appreciation programs are recommended. |
| **Potential Loyalist (12%)**| Moderate (~50 days)         | Moderate (~100 purchases)          | Moderate (~7% of revenue)       | Customers with promising engagement. Targeted incentives may convert them into loyal buyers. |
| **New Customers (8%)**      | Moderately recent (~40 days) | Low frequency (~50 purchases)      | Low (~3% of revenue)            | Newly acquired users showing early signs of interest. Retention efforts such as welcome flows and personalized offers are needed. |
| **Promising (4%)**          | Moderate (~60–70 days)       | Moderate (~50–80 purchases)        | Low (~4% of revenue)            | These customers may return but show weak commitment. Follow-up campaigns and nudges may increase loyalty. |
| **Need Attention (6%)**     | High (~120+ days)            | Low to moderate (~50 purchases)    | Low (~3–4% of revenue)          | Previously engaged customers whose activity is declining. Risk of defection to competitors — should be reactivated. |
| **At Risk (11%)**           | High (~120 days)             | Moderate (~100 purchases)          | High (~10–14% of revenue)       | Former high-value customers who are disengaging. Immediate win-back strategies are required. |
| **About to Sleep (4%)**     | High (~100 days)             | Low (~30 purchases)                | Low (~3% of revenue)            | Customers on the verge of churn. Re-engagement is urgent before they become inactive. |
| **Cannot Lose Them (3%)**   | Very high (~180+ days)       | Moderate (~100 purchases)          | Moderate (~4–5% of revenue)     | Past big spenders now inactive. High-priority group for targeted retention offers. |
| **Hibernating (18%)**       | Very high (~200 days)        | Very low (~10–20 purchases)        | Very low (~2% of revenue)       | Dormant customers who have not engaged for a long time. Consider reactivation or list pruning. |
| **Lost Customers (9%)**     | Extremely high (220+ days)   | Extremely low (~5–10 purchases)    | Very low (~1–2% of revenue)     | Nearly lapsed customers with minimal purchase history. Only strong and tailored outreach may bring them back. |

> 🔍 These insights provide a strategic foundation for tailored marketing initiatives — focusing on retention for high-value customers (e.g., Champions, At Risk) and nurturing potential segments (e.g., Potential Loyalists, Promising).

---

### 📍 Part 2: Identify Most Influential RFM Metric

To determine which RFM metric (Recency, Frequency, or Monetary) is most strongly tied to customer value (Monetary), we use the following visualizations:

---

#### 1️⃣ Correlation Heatmap

<img width="573" height="398" alt="image" src="https://github.com/user-attachments/assets/04171e86-fb0c-4f64-9677-c9e7b0d7b593" />

---

#### 2️⃣ Boxplots of Monetary vs. R/F/M Scores

<img width="1765" height="486" alt="image" src="https://github.com/user-attachments/assets/f485ea5d-47a5-4001-aba7-17e087928315" />

---

## 📊 Key Findings

| Analysis Type             | Key Observations                                                                                                                                                                                                                                                                                             |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 🔺 **Correlation Matrix** | - Moderate positive correlation between Frequency and Monetary (0.43) → suggests that frequent buyers tend to spend more. <br> - Recency has weak negative correlation with both Frequency and Monetary, meaning more recent customers are not necessarily frequent or high-spending.                        |
| 📦 **Boxplots**           | - Customers with high **Monetary** and **Frequency** scores show strong alignment with high actual spending. <br> - **Monetary score** shows clearest separation between spend levels, followed by Frequency. <br> - Recency score has weaker variation in spending, with overlapping medians across scores. |


---

## 🧠 IV. Final Conclusion & Recommendations

### 🧭 Customer Grouping & Marketing Strategies

Based on RFM segments, we consolidate the 11 customer types into 4 strategic customer groups. Each group represents a different level of customer engagement and value. Below are the suggested marketing strategies tailored to each:

| Group                     | Included Segments                                                                 | Characteristics                                                                                           | Marketing Strategy                                                                                      |
|---------------------------|------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **1. High-Value & Engaged**     | Champions, Loyal                                                                 | Recently active, purchase frequently, and contribute the most to revenue.                                 | ✅ Exclusive loyalty programs<br>✅ Early access to promotions<br>✅ Personalized offers & appreciation campaigns |
| **2. Growth Opportunities**     | Potential Loyalist, New Customers, Promising                                     | Medium to recent activity, not yet loyal but show potential to convert.                                   | 📈 Targeted email nurture sequences<br>📈 Welcome offers or onboarding journeys<br>📈 Encourage repeat purchases |
| **3. At Risk / Churning**       | At Risk, Need Attention, About to Sleep, Cannot Lose Them                        | Previously active but showing signs of disengagement.                                                     | ⚠️ Win-back campaigns (discounts, reminders)<br>⚠️ Re-engagement surveys<br>⚠️ Urgency-based promotions |
| **4. Inactive / Low-Value**     | Hibernating, Lost Customers                                                      | Very little activity or purchases long ago. Low contribution to revenue.                                  | 💤 Periodic reactivation campaigns<br>💤 Sunset or deprioritize in marketing efforts<br>💤 Test reactivation with limited offers |

> 🎯 By focusing efforts on the **High-Value & Engaged** and **Growth Opportunities** groups, while running targeted reactivation for **At Risk**, businesses can maximize customer lifetime value and marketing ROI.

---

### 📌 RFM Component Importance
| RFM Component | Priority Level | Justification                                                                                                                                                               |
| ------------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Monetary**  | ⭐️⭐️⭐️ High    | Strongest separation in actual customer value (from boxplots) and moderate correlation with Frequency. Excellent indicator of a customer’s long-term value.                 |
| **Frequency** | ⭐️⭐️ Medium    | Positively correlated with Monetary and shows decent stratification. Frequent buyers are likely to bring sustained revenue.                                                 |
| **Recency**   | ⭐️ Low         | Weakest correlation and inconsistent monetary patterns. May not be a strong standalone predictor in this dataset but still relevant in specific churn detection strategies. |

#### ✅ Strategic Takeaways
+ Prioritize **Monetary** score when defining valuable customer segments for high-ROI campaigns.

+ Use **Frequency** score to identify loyal and consistent buyers for retention initiatives.

+ Treat **Recency** as a supporting metric in churn-prevention strategies rather than a lead indicator for top-value segmentation.

---


