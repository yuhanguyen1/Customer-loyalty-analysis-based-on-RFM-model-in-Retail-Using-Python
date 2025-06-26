# Customer loyalty analysis based on RFM model in Retail Using Python
Conducted customer loyalty analysis for a retail business using the RFM model in Python; applied Numpy and Pandas for data processing on ~541k sales records, and visualized key patterns with Matplotlib and Seaborn to uncover actionable customer segments.

Author: Nguyen Anh Huy

Date: 18/05/2025

Tools Used: Python (Jupiter Notebook)

## Table of Contents

[I. Background & Overview](https://github.com/yuhanguyen/RFM-Analysis?tab=readme-ov-file#i-background--overview)

[II. Dataset Description & Data Structure](https://github.com/yuhanguyen/RFM-Analysis?tab=readme-ov-file#ii-dataset-description--data-structure)

[III. Main Process](https://github.com/yuhanguyen/RFM-Analysis?tab=readme-ov-file#iii-main-process)

[IV. Final Conclusion & Recommendations](https://github.com/yuhanguyen/RFM-Analysis?tab=readme-ov-file#iv-final-conclusion--recommendations)

## I. Background & Overview

### Context
SuperStore Company is a global retail company. So the company has a lot of customers. On the occasion of Christmas and New Year, the Marketing Department wants to run marketing campaigns to thank customers who have supported the company over the past time. As well as exploit customers with the potential to become loyal customers. 

However, the Marketing Department has not been able to group each customer this year because the data set is too large to be processed manually like previous years, so the Data Analysis Department is asked to support the implementation of a segmentation problem for each customer to implement each marketing program suitable for each customer group.

The Marketing Director also proposed using the RFM model, but in the past, when the company was small, the team could calculate and classify it themselves using Excel. Currently, the amount of data is too large, so the Data Department wants to build a flow to evaluate Segmentation through Python programming.

### Objective
This project uses Python to analyze the Ecommerce retail dataset to:

✔️ Segmentate the customers into groups and create suitable marketing campaigns for each group.

✔️ Decide which metric in the RFM model is the best for retail companies like Superstore.

Who is this project for?

✔️ Data analysts & business analysts

✔️ Marketing Director & stakeholders

## II. Dataset Description & Data Structure

This is a transnational data set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail. The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers. Here is the data description:

**ecommerce retail.xlsx**

| Column | Data type | Description |
| :---: | :---: | :---: |
| InvoiceNo | OBJECT | Invoice number. Nominal, a 6-digit integral number uniquely assigned to each transaction. If this code starts with letter 'C', it indicates a cancellation. |
| StockCode | OBJECT | Product (item) code. Nominal, a 5-digit integral number uniquely assigned to each distinct product. |
| Description | OBJECT | Product (item) name. Nominal. |
| Quantity | INTEGER | The quantities of each product (item) per transaction. Numeric. |
| InvoiceDate | DATETIME | Invoice Date and time. Numeric, the day and time when each transaction was generated. |
| UnitPrice | FLOAT | Unit price. Numeric, Product price per unit in sterling. |
| CustomerID | FLOAT | Customer number. Nominal, a 5-digit integral number uniquely assigned to each customer. |
| Country | OBJECT | Country name. Nominal, the name of the country where each customer resides. |

## III. Main Process

### Import Package, dataset

![image](https://github.com/user-attachments/assets/46b947ee-c887-41d6-adc4-f64184413559)

### EDA

**EDA Summary**

**1. Convert data type**

Convert data type is not suitable

**2. Remove invalid value data**

Remove invalid data according to the following conditions:

Quantity > 0

UnitPrice > 0

InvoiceNo starts with "C" (order is canceled)

**3. Handle missing data**

Action: Remove missing CustomerID columns

**4. Handle duplicate data**

Action: Remove duplicate data


**Get info about data types & data values**

![image](https://github.com/user-attachments/assets/aeda2c8f-2413-4da5-91fa-fffbd72536bd)

![image](https://github.com/user-attachments/assets/2d7fb6d8-01dc-4ee8-b4e2-6178bef6749d)

![image](https://github.com/user-attachments/assets/2bd65a6e-613b-4464-9253-95d3448d2cf3)

![image](https://github.com/user-attachments/assets/ecacfd81-aaee-40ea-aa55-4de6a4dc3079)

**Check missing values & duplicates**

![image](https://github.com/user-attachments/assets/90cdd79e-36ee-495d-8a5b-3a6a7891090a)

![image](https://github.com/user-attachments/assets/31dbc848-b967-4592-9ca7-40c54af54221)

![image](https://github.com/user-attachments/assets/08cde631-cd56-452c-b271-900ad2221e72)


### Data Processing

![image](https://github.com/user-attachments/assets/c114c063-3273-4f18-a797-873eb267a2f5)

![image](https://github.com/user-attachments/assets/2842d5c0-5c63-4ce1-a473-f4d13ba9e95a)

![image](https://github.com/user-attachments/assets/7e3636e0-e64a-413b-9da5-1462c90f6453)

![image](https://github.com/user-attachments/assets/851ebce4-25fd-4ce4-afd1-7ee21c7d9142)

![image](https://github.com/user-attachments/assets/b5e1ebd6-1569-4fd9-85f4-115c884831dd)

### Visualization

![image](https://github.com/user-attachments/assets/34b03cb0-6e1a-460d-a7bc-8c39a45b28eb)

Result:

![image](https://github.com/user-attachments/assets/90a9097e-c02b-486d-9466-899bd672ca17)

Result:

![image](https://github.com/user-attachments/assets/e22970a7-583f-4324-8993-47c5aeb6ffee)

![image](https://github.com/user-attachments/assets/5f321f5a-9468-47e3-96e9-412364806e35)

![image](https://github.com/user-attachments/assets/ece50a1a-e560-4b2b-acb7-4ebf4064b0df)


## IV. Final Conclusion & Recommendations

### Customer Segmentation

Hibernating customers and Lost customers account for a high proportion of the customer structure. However, this group does not account for a large proportion of revenue

**Action**: Implement react-out campaigns, send emails to reconnect with this customer group, or can be ignored

Champions and Loyal customers are customer groups that are loyal to the brand, accounting for the majority of revenue.

**Action**: Implement campaigns such as lucky draws, upsale programs that bring attractive incentives

Potential Loyalist, Need attention and Promising customer groups are also very large and account for a fairly high proportion of revenue

**Action**: Implement campaigns to promote loyal customers, member incentives to turn them into loyal customers

### Best Metric in RFM model

For a retail model like SuperStore, the most important thing is that customers return to buy frequently (Recency) because it shows the level of customer attachment to the brand. A customer who has purchased many times in the past but has not purchased for a long time can still be in the group of customers who have left.

The frequency of customer purchases (Frequency) is also very important because it helps identify customers who are loyal to the brand.

Spending on orders (Monetary) can be affected by other factors such as promotions, combos, so it often does not reflect the most accurate status of the company.

Therefore, I recommend that the Marketing and Sales teams of SuperStore should pay the most attention to the Recency index, followed by Frequency and Monetary.
