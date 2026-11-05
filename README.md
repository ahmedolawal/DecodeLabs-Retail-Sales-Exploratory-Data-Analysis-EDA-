# DecodeLabs-Retail-Sales-Exploratory-Data-Analysis-EDA-
This project explores a retail transactions dataset with Python to uncover the story behind the numbers. It demonstrates how structured exploratory data analysis (EDA) can turn a static table of sales records into useful evidence about revenue, product performance, transaction behaviour, distributions, relationships and changes over time.

Rather than jumping straight to predictive modelling or dashboard development, the analysis focuses on asking the data disciplined questions:
- What does the dataset contain, and how complete and reliable is it?
- How are quantities, unit prices, basket sizes and transaction values distributed?
- Which products contribute most and least to revenue and sales volume?
- How do sales and revenue change daily and monthly?
- Which numerical variables move together?
- Are there unusual transactions that deserve further investigation?
The work is contained in the Jupyter notebook DecodeLabs- Project 2 Python Final.ipynb.

# Business context
Retail teams need more than a total-sales figure. They need to understand what is selling, how much customers buy, which products contribute to revenue, whether performance is changing over time and whether unusual transactions could affect decisions.

This Exploratory Data Analysis (EDA) provides an initial evidence base for those questions. It is descriptive and diagnostic analysis: it identifies patterns and questions worth investigating, but it does not establish causation or predict future sales.

## Dataset at a glance
The notebook analyses 1,200 transaction records and 14 columns, covering 1 January 2023 to 30 June 2025.
Attribute	Value observed in the notebook
Transaction records	1,200
Columns	14
Unique products	7
Date coverage	2023-01-01 to 2025-06-30
Duplicate rows	0
Missing values	309, all in CouponCode
Total revenue (TotalPrice)	1,264,761.96
Average transaction value	1,053.97
Total quantity sold	3,535


Note: The dataset does not specify a currency in the notebook, so revenue figures are shown without a currency symbol. The 309 missing CouponCode values represent approximately 25.8% of records; the notebook does not establish whether these mean that no coupon was used or that coupon information was not captured.

Dataset fields
The 14 fields available in the notebook are:
Column	Description
OrderID	Transaction/order identifier
Date	Order date
CustomerID	Customer identifier
Product	Product purchased
Quantity	Number of units purchased
UnitPrice	Price per unit
ShippingAddress	Shipping address recorded for the order
PaymentMethod	Payment method
OrderStatus	Order fulfilment/status value
TrackingNumber	Shipment tracking identifier
ItemsInCart	Number of items recorded in the cart
CouponCode	Coupon/promotion code, where present
ReferralSource	Recorded referral or acquisition source
TotalPrice	Transaction total used as the revenue measure


# Analytical workflow
The notebook follows an EDA workflow, moving from data understanding to deeper business interpretation.
## 1. Data inspection and quality checks
- Loaded the Excel dataset into pandas.
- Inspected sample records, dimensions, column names and data types.
- Checked missing values, unique-value counts and duplicate rows.
- Generated descriptive statistics to understand the numerical fields.
Observed quality result: 1,200 rows and 14 columns; no fully duplicated rows; 309 missing values in CouponCode, with no missing values reported in the other columns in the initial check.
## 2. Univariate analysis — understanding individual variables
- Used summary statistics (mean, median, standard deviation, minimum and maximum).
- Examined distributions with histograms and density plots.
- Used boxplots to inspect spread and potential extreme values.
- Reviewed product frequency and percentage distribution.
This stage helps distinguish typical transaction behaviour from skewed distributions and unusual observations.
## 3. Bivariate and multivariate analysis — exploring relationships
- Compared Quantity with TotalPrice using scatter and regression plots.
- Examined correlations among numerical variables.
- Compared average and total revenue across products.
- Used cross-tabulation and a heatmap to examine Product against Category where available in the analysis.
- Used a pair plot to inspect relationships among quantity, unit price and total price.
Correlation and visual association are treated as evidence of relationships, not proof that one variable causes another.
## 4. Time-series exploration
- Sorted transactions by date.
- Aggregated revenue by day and month.
- Calculated cumulative revenue.
- Calculated month-on-month revenue growth using percentage change.
- Examined monthly quantity sold.
These views help reveal changes and volatility over the observed period. The notebook's monthly quantity calculation groups by calendar month number, so it combines the same month across different years rather than showing a separate month-year series.
## 5. Product and business performance
Grouped the data by product to calculate:
- Total and average quantity sold.
- Total and average transaction revenue.
- Average unit price.
- Transaction count.
The notebook also uses ranking, pivot tables, value_counts(), groupby(), agg() and nlargest() / nsmallest() to summarise performance.
## 6. Outlier detection
Applied the interquartile range (IQR) rule to TotalPrice:
- \(Q1 = 410.52\)
- \(Q3 = 1,578.475\)
- \(IQR = Q3 - Q1\)
- Outlier boundaries: \(Q1 - 1.5 \times IQR\) and \(Q3 + 1.5 \times IQR\)
The project identified 8 high-value TotalPrice observations using this rule. These should be investigated as potentially exceptional transactions, not automatically deleted or labelled as errors.

## Key findings 

### Overall performance
- Total revenue: 1,264,761.96
- Average transaction value: 1,053.97
- Total quantity sold: 3,535
- Transactions: 1,200
- Unique products: 7
Product revenue ranking
Rank	Product	Total revenue
1	Chair	195,620.11
2	Printer	195,612.61
3	Laptop	192,126.56
4	Tablet	186,568.95
5	Monitor	175,651.41
6	Desk	167,459.93
7	Phone	151,722.39


Chair generated the highest recorded revenue, narrowly ahead of Printer (a difference of 7.50). Phone generated the lowest recorded revenue.

# Product volume and transaction counts
- Chair recorded the highest total quantity sold: 562 units.
- Printer had the highest transaction count: 181 transactions.
- Phone had the lowest total quantity sold: 411 units, and the lowest transaction count: 156.
Revenue leadership and volume leadership are not identical: the product with the highest revenue is not necessarily the one with the highest transaction count.

# Revenue over time
Monthly revenue growth across the period were analysed, month-on-month changes are variable, with both positive and negative months. The largest positive monthly growth shown in the output is 143.89% (June 2024); the largest decline shown is -45.68% (September 2023).

These are changes against the immediately preceding month, not year-on-year growth. Percentage changes can also be sensitive to the size of the previous month's revenue.

# Data quality and unusual observations
- No fully duplicated records were detected.
- CouponCode is the only field with missing values in the initial missing-value check.
- Eight TotalPrice observations were flagged by the IQR rule. They warrant contextual review before any treatment decision.

## Tools and libraries
- Python — analysis and data manipulation
- Jupyter Notebook — interactive analytical workflow
- pandas — data loading, cleaning, aggregation and summarisation
- NumPy — numerical operations
- Matplotlib — charts and visual exploration
- Seaborn — statistical visualisations
Repository structure
A simple suggested GitHub structure is:
DecodeLabs-Retail-Sales-EDA/
├── data/
│   └── Decode_Lab.xlsx
├── notebooks/
│   └── DecodeLabs- Project 2 Python Final.ipynb
├── README.md
└── requirements.txt
The notebook currently reads the Excel file from a machine-specific Windows path. For a portable repository, place the dataset in data/ and update the loading cell to use a relative path, 

# Limitations and interpretation notes
- The notebook's outputs describe the dataset supplied for this exercise; they should not be treated as independently verified company-wide financial results.
- No currency is stated for TotalPrice.
- Missing coupon codes are not automatically equivalent to transactions with no coupon.
- IQR flags identify statistical extremes, not necessarily incorrect records.
- The analysis is primarily descriptive. It does not test causal hypotheses, forecast revenue or evaluate a predictive model.
- The notebook includes a Product-versus-`Category` cross-tabulation, although Category is not present in the 14-column schema printed earlier. Confirm that the source data version includes this field, or revise that cell before rerunning the notebook from a clean session.
- The notebook contains repeated calculations and a machine-specific input path; these are good candidates for cleanup to improve reproducibility.

## Potential next steps
1. Strengthen data validation: explicitly validate date parsing, numeric fields, transaction totals and categorical values.
2. Clarify order-status performance: compare shipped, delivered, cancelled and returned transactions, and define whether revenue should include all statuses.
3. Investigate customer behaviour: examine repeat customers, customer-level revenue and basket-size patterns using CustomerID.
4. Improve time analysis: compare month-year periods consistently, add rolling averages and investigate seasonality.
5. Deepen acquisition analysis: compare revenue and order volume by ReferralSource, PaymentMethod and coupon usage, accounting for missing coupon data.
6. Create a concise findings report: pair each chart with a clear observation, its business implication and a follow-up question.

## Project outcome
This project demonstrates the core analytical discipline behind effective EDA: 
- inspect the data
- test its quality
- understand distributions
- explore relationships
- investigate outliers
- analyse trends and
- translate the results into business-facing observations.

## The central takeaway: 
Meaningful analytics begins before the dashboard or model. It begins by asking better questions of the data and following the evidence wherever it leads.
Project notebook: DecodeLabs- Project 2 Python Final.ipynb


# Exploratory Data Analysis

## Importing the Required Libraries
```
import numpy as np
import pandas as pd
import seaborn as sns
from matplotlib import pyplot as plt
%matplotlib inline
```

```
DecodeLabs_df = pd.read_excel(r"C:\Users\filepath.xlsx")
DecodeLabs_df.head()
```

<img width="1037" height="198" alt="image" src="https://github.com/user-attachments/assets/a9536747-2cf5-4a15-b523-793ea277cac8" />

# Checking for null values
```
DecodeLabs_df.isnull().sum()
```
<img width="213" height="221" alt="image" src="https://github.com/user-attachments/assets/944f6da0-93ca-4859-81bc-c460c86efb55" />

# Checking the shape of the dataframe
```
DecodeLabs_df.shape
```
<img width="152" height="26" alt="image" src="https://github.com/user-attachments/assets/fadacac7-4889-49c0-9629-dbefab2f1207" />

# checking for number of unique values in the target
```
DecodeLabs_df.nunique()
```
<img width="188" height="229" alt="image" src="https://github.com/user-attachments/assets/bbddeb98-92d8-4235-90dd-e99f8a9a25a7" />

# Count duplicate rows
```
print("Number of duplicate rows:", DecodeLabs_df.duplicated().sum())
```
<img width="219" height="28" alt="image" src="https://github.com/user-attachments/assets/ffaca8cd-5ffc-4b81-a36c-1ccf51fa4a57" />

# checking for the stastistics
```
DecodeLabs_df.describe()
```
<img width="447" height="195" alt="image" src="https://github.com/user-attachments/assets/c1857f5d-246b-4d9f-a730-d6d841015261" />

```
numeric_df = DecodeLabs_df.select_dtypes(include='number')
numeric_df.agg(['mean', 'median', 'std', 'min', 'max'])
```
<img width="388" height="123" alt="image" src="https://github.com/user-attachments/assets/83dff35c-7635-4a08-9fe4-337bb8148e56" />


```
numeric_df = DecodeLabs_df.select_dtypes(include='number')
numeric_df.agg(['mean', 'median', 'std', 'min', 'max'])
```
<img width="317" height="127" alt="image" src="https://github.com/user-attachments/assets/184e872f-8a18-46dc-b2d8-ea375b166f1b" />

### Analysis of Data Fields
```
DecodeLabs_df.dtypes
```
<img width="226" height="215" alt="image" src="https://github.com/user-attachments/assets/5953cd5f-2a1f-44b0-8dde-956413d8246a" />

```
DecodeLabs_df.columns
```
<img width="448" height="73" alt="image" src="https://github.com/user-attachments/assets/22b51ee6-da1a-4698-84fe-79ae9ea7bd23" />

## Correlation heatmap
#### This helps identify variables that move together.

```
# Keep only numeric columns
numeric_df = DecodeLabs_df.select_dtypes(include=['int64', 'float64'])

# Correlation matrix
corr_matrix = numeric_df.corr(method='pearson')

# Plot heatmap
plt.figure(figsize=(14,10))

sns.heatmap(
    corr_matrix,
    annot=True,
    fmt='.2f',
    cmap='RdYlGn',
    center=0,
    linewidths=0.5,
    annot_kws={'size':8}
)

plt.title('Correlation Matrix', fontsize=16, fontweight='bold')
plt.xticks(rotation=45, ha='right')
plt.yticks(rotation=0)

plt.tight_layout()
plt.show()
```

<img width="550" height="436" alt="image" src="https://github.com/user-attachments/assets/1c9aad20-eff7-4e88-bb72-b22c5efecd7a" />

# Trend analysis of Decodelabs Revenue
```
daily_sales = DecodeLabs_df.groupby(
    DecodeLabs_df['Date'].dt.date
)['TotalPrice'].sum()

daily_sales.plot(figsize=(14, 6))

plt.title('Daily Sales Trend')
plt.xlabel('Date')
plt.ylabel('Sales Revenue')
plt.show()
```
<img width="872" height="401" alt="image" src="https://github.com/user-attachments/assets/9b1f660c-1c8f-4d6d-9555-02951e7b5aff" />

### Decodelabs Monthly Revenue Trend
```
monthly_revenue = DecodeLabs_df.groupby(
    DecodeLabs_df['Date'].dt.to_period('M')
)['TotalPrice'].sum()

monthly_revenue.plot(
    figsize=(14, 6),
    marker='o'
)

plt.title('Monthly Revenue Trend')
plt.xlabel('Month')
plt.ylabel('Total Revenue')
plt.xticks(rotation=45)
plt.show()
```
<img width="879" height="431" alt="image" src="https://github.com/user-attachments/assets/9d5381c7-68ff-461e-99dc-0d6166f4b857" />

## Analysis of Count of Products
```
plt.figure(figsize=(16,6))

ax = sns.countplot(
    data=DecodeLabs_df,
    x='Product',
    color='steelblue'
)

ax.bar_label(ax.containers[0])

plt.title('Count of Products')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```
<img width="991" height="365" alt="image" src="https://github.com/user-attachments/assets/90f67a74-69cb-4712-a7de-6ddd334a5fb6" />

## Analysis of Monthly Quantity of Product Sold
```
monthly_quantity = DecodeLabs_df.groupby(
    DecodeLabs_df['Date'].dt.month
)['Quantity'].sum()

ax = monthly_quantity.plot(
    kind='bar',
    figsize=(12, 5),
    color='steelblue'
)

# Add data labels
for container in ax.containers:
    ax.bar_label(container, fmt='%.0f', padding=3)

plt.title('Monthly Quantity Sold')
plt.xlabel('Month')
plt.ylabel('Quantity Sold')
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()
```
<img width="886" height="349" alt="image" src="https://github.com/user-attachments/assets/b78e2028-c43e-434c-8d25-061c0fa521e1" />

### Average Revenue by Product
```
plt.figure(figsize=(14, 6))

ax = sns.barplot(
    data=DecodeLabs_df,
    x='Product',
    y='TotalPrice',
    estimator='mean',
    errorbar=None
)

ax.bar_label(ax.containers[0], fmt='%.0f')

plt.title('Average Revenue by Product')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```
<img width="989" height="413" alt="image" src="https://github.com/user-attachments/assets/c594e192-2d8d-4ffc-9894-47d8c8607f60" />

# Analysis of Revenue by Product
```
DecodeLabs_df.groupby('Product')['TotalPrice'].sum().sort_values(
    ascending=False
)
```
<img width="249" height="128" alt="image" src="https://github.com/user-attachments/assets/eeb10ec1-c223-47ec-8899-b425ef6578c8" />

```
pd.pivot_table(
    DecodeLabs_df,
    index='Product',
    values=['Quantity', 'TotalPrice'],
    aggfunc={
        'Quantity': 'sum',
        'TotalPrice': 'sum'
    }
)
```
<img width="193" height="188" alt="image" src="https://github.com/user-attachments/assets/88915adf-c7f0-4f71-b4ab-0bad7e13bf28" />

## Summary of Revenue by Product
```
product_revenue = DecodeLabs_df.groupby('Product')['TotalPrice'].sum().sort_values(
    ascending=False
)

ax = product_revenue.plot(
    kind='bar',
    figsize=(14,6),
    color='teal'
)

ax.bar_label(ax.containers[0], fmt='£{:,.0f}')

plt.title('Revenue by Product')
plt.xlabel('Product')
plt.ylabel('Revenue (£)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```
<img width="988" height="405" alt="image" src="https://github.com/user-attachments/assets/002c8edf-686b-40d1-a0c3-a38a7c87efe8" />

## Product Statistics
```
product_analysis = DecodeLabs_df.groupby('Product').agg(
    Total_Quantity=('Quantity', 'sum'),
    Average_Quantity=('Quantity', 'mean'),
    Total_Revenue=('TotalPrice', 'sum'),
    Average_Revenue=('TotalPrice', 'mean'),
    Average_UnitPrice=('UnitPrice', 'mean'),
    Transaction_Count=('Product', 'count')
).sort_values(
    by='Total_Revenue',
    ascending=False
)

print(product_analysis)
```
<img width="452" height="271" alt="image" src="https://github.com/user-attachments/assets/eca717dd-ed7c-4fce-bb36-5ec55282b512" />

# Overall Business Performance
```
print('Total Revenue:', DecodeLabs_df['TotalPrice'].sum())

print('Average Revenue:', DecodeLabs_df['TotalPrice'].mean())

print('Total Quantity Sold:', DecodeLabs_df['Quantity'].sum())

print('Total Transactions:', len(DecodeLabs_df))

print('Number of Unique Products:', DecodeLabs_df['Product'].nunique())
```
<img width="226" height="88" alt="image" src="https://github.com/user-attachments/assets/95d050e1-7e3b-4f12-ba76-7b80a7a6ee7f" />





















 
