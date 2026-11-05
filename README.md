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

# Dataset fields
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

## Rolling Revenue
```
DecodeLabs_df['TotalPrice'] = pd.to_numeric(DecodeLabs_df['TotalPrice'], errors='coerce').fillna(0)
DecodeLabs_df = DecodeLabs_df.sort_values('Date').reset_index(drop=True)
DecodeLabs_df['Cumulative_Revenue'] = DecodeLabs_df['TotalPrice'].cumsum()

DecodeLabs_df[['Date', 'TotalPrice', 'Cumulative_Revenue']].head(10)
```
<img width="321" height="239" alt="image" src="https://github.com/user-attachments/assets/673b4158-2ec7-4d32-a0aa-7eba314ac8dd" />

## Analysis of Change in Revenue over the period considered
```
monthly_revenue = DecodeLabs_df.groupby(
    DecodeLabs_df['Date'].dt.to_period('M')
)['TotalPrice'].sum()

monthly_growth = monthly_revenue.pct_change() * 100

print(monthly_growth)
```
<img width="265" height="428" alt="image" src="https://github.com/user-attachments/assets/08bcef06-d45a-4e4b-9ab3-6934cfca278f" />

## Analysis of decodelabs Monthly Revenue Growth
```
monthly_revenue = DecodeLabs_df.groupby(
    DecodeLabs_df['Date'].dt.to_period('M')
)['TotalPrice'].sum()

monthly_growth = monthly_revenue.pct_change() * 100

fig, ax = plt.subplots(figsize=(12, 6))

bars = ax.bar(
    monthly_growth.index.astype(str),
    monthly_growth,
    color=['green' if x >= 0 else 'red' for x in monthly_growth.fillna(0)]
)

ax.bar_label(bars, fmt='%.1f%%', padding=3)

ax.axhline(0, color='black', linewidth=0.8)
ax.set_title('Monthly Revenue Growth (%)')
ax.set_ylabel('Growth vs Previous Month (%)')

plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```
<img width="890" height="440" alt="image" src="https://github.com/user-attachments/assets/4c224ac9-0446-441b-bbe3-9db09bfdaa27" />

## Histogram - Distribution of the data in Field with Numeric Values
```
plt.figure(figsize=(12, 17))

plt.subplot(5, 2, 1)
sns.histplot(data=DecodeLabs_df, x='Date', kde=True)
plt.title('Distribution of Date')

plt.subplot(5, 2, 2)
sns.histplot(data=DecodeLabs_df, x='Quantity', kde=True)
plt.title('Distribution of Quantity')

plt.subplot(5, 2, 3)
sns.histplot(data=DecodeLabs_df, x='UnitPrice', kde=True)
plt.title('Distribution of Unit Price')

plt.subplot(5, 2, 4)
sns.histplot(data=DecodeLabs_df, x='ItemsInCart', kde=True)
plt.title('Distribution of Items in Cart')

plt.subplot(5, 2, 5)
sns.histplot(data=DecodeLabs_df, x='TotalPrice', kde=True)
plt.title('Distribution of Total Price')

plt.tight_layout()
plt.show()
```

<img width="887" height="259" alt="image" src="https://github.com/user-attachments/assets/85f1e1f5-6ae8-4979-85cb-8a6368560fa0" />
<img width="884" height="512" alt="image" src="https://github.com/user-attachments/assets/3ae18b2c-0b85-4d2c-9409-daf314cbcb83" />

# Descriptive Statistics

## Mean
```
DecodeLabs_df.select_dtypes(include='number').mean()
```
<img width="264" height="100" alt="image" src="https://github.com/user-attachments/assets/30cf62d7-f3d3-4583-8719-f523519b47ac" />

## Median
```
DecodeLabs_df.select_dtypes(include='number').median()
```
<img width="231" height="93" alt="image" src="https://github.com/user-attachments/assets/cecc2d1c-6b09-4cfc-9e14-7f3a5bca1556" />

## Count
```
DecodeLabs_df.count()
```
<img width="237" height="242" alt="image" src="https://github.com/user-attachments/assets/d1a09e08-bbf5-4c6a-84ed-77014e81a7ef" />

## Minimum values
```
DecodeLabs_df.select_dtypes(include='number').min()
```
<img width="251" height="86" alt="image" src="https://github.com/user-attachments/assets/7e95a4ac-bc3b-45ee-9b7a-8cc466644b9c" />

## Maximum values
```
DecodeLabs_df.select_dtypes(include='number').max()
```
<img width="264" height="101" alt="image" src="https://github.com/user-attachments/assets/5baf3e6b-8601-46a0-9e32-5401bbc22af2" />

## Standard Deviation
```
DecodeLabs_df.select_dtypes(include='number').std()
```
<img width="305" height="100" alt="image" src="https://github.com/user-attachments/assets/968fee57-1029-401d-9c22-41d76002b41b" />

## Variance
```
DecodeLabs_df.select_dtypes(include='number').var()
```
<img width="219" height="98" alt="image" src="https://github.com/user-attachments/assets/ad0d57b2-db74-454b-ab8b-dc251c038b77" />

## Total Price Distribution Plot

```
# TotalPrice (must be numeric and clean i.e. free from invalid data)
DecodeLabs_df['TotalPrice'] = pd.to_numeric(DecodeLabs_df['TotalPrice'], errors='coerce')
plot_data = DecodeLabs_df['TotalPrice'].replace([float('inf'), float('-inf')], pd.NA).dropna()

# Distribution plot
plt.figure(figsize=(10, 6))
sns.histplot(plot_data, kde=True, bins=30)
plt.title('Distribution of Total Price')
plt.xlabel('Total Price')
plt.ylabel('Frequency')
plt.show()
```
<img width="628" height="392" alt="image" src="https://github.com/user-attachments/assets/3a630bf0-7845-4600-9b0a-db49c310bc15" />

## Total Price Density
```
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

DecodeLabs_df['TotalPrice'] = pd.to_numeric(DecodeLabs_df['TotalPrice'], errors='coerce')
plot_data = DecodeLabs_df['TotalPrice'].replace([float('inf'), float('-inf')], pd.NA).dropna()

plt.figure(figsize=(10, 6))
sns.kdeplot(x=plot_data, fill=True)
plt.title('Density of Total Price')
plt.xlabel('Total Price')
plt.ylabel('Density')
plt.show()
```
<img width="647" height="401" alt="image" src="https://github.com/user-attachments/assets/29201f6f-7766-459c-9e28-ebbd0de989fa" />

## Frequency Counts
```
DecodeLabs_df['Product'].value_counts()
```
<img width="253" height="143" alt="image" src="https://github.com/user-attachments/assets/77fad86f-e7a7-45b5-94cd-8ee3b822dd75" />

## Percentage Distribution
```
DecodeLabs_df['Product'].value_counts(normalize=True) * 100
```
<img width="252" height="139" alt="image" src="https://github.com/user-attachments/assets/da8d3dad-8875-46b6-94db-9efa4d13f877" />

## Number of unique products
```
DecodeLabs_df['Product'].nunique()
```
<img width="194" height="32" alt="image" src="https://github.com/user-attachments/assets/af7caba5-22c3-441f-b366-f0988468b843" />

## Bivariate Analysis – Identifying Relationships

## Categorical vs categorical variables

### Using cross-tabulation to investigate relationships between Categories

#### Analysis of Product by Order Status

```
pd.crosstab(
    DecodeLabs_df['Product'],
    DecodeLabs_df['OrderStatus']
)
```

<img width="367" height="188" alt="image" src="https://github.com/user-attachments/assets/f537ec5c-d23e-4105-acd0-9d9bc7b59617" />

### Analysis of Product by Order Status in Percentage
```
pd.crosstab(
    DecodeLabs_df['Product'],
    DecodeLabs_df['OrderStatus'],
    normalize='index'
).mul(100).round(1)
```

<img width="371" height="177" alt="image" src="https://github.com/user-attachments/assets/fe38203b-014d-4465-8eca-8cf12c79d498" />

### Analysis of Product by Coupon Code
```
pd.crosstab(
    DecodeLabs_df['Product'],
    DecodeLabs_df['CouponCode']
)
```
<img width="281" height="189" alt="image" src="https://github.com/user-attachments/assets/831d5bd8-3c80-4ca7-af12-d871f22ec93e" />

### Analysis of Product by Referral Source

```
pd.crosstab(
    DecodeLabs_df['Product'],
    DecodeLabs_df['ReferralSource']
)
```
<img width="354" height="194" alt="image" src="https://github.com/user-attachments/assets/ec52f8a3-3438-4702-b072-c7d9342e0433" />

### Analysis of Product by Referral Source in Percentage
```
pd.crosstab(
    DecodeLabs_df['Product'],
    DecodeLabs_df['ReferralSource'],
    normalize='index'
).mul(100).round(1)
```
<img width="384" height="187" alt="image" src="https://github.com/user-attachments/assets/74c2b953-4438-4966-b7d9-5620ecb3b72f" />

# Multivariate analysis – understanding multiple variables
### Multivariate analysis examines three or more variables simultaneously.

## Pair Plot
```
sns.pairplot(
    DecodeLabs_df,
    vars=['Quantity', 'UnitPrice', 'TotalPrice'],
    diag_kind='hist'
)

plt.show()
```
<img width="548" height="545" alt="image" src="https://github.com/user-attachments/assets/280f1838-1096-464b-a32c-abd28da75336" />

This helps you identify:
- Positive relationships.
- Negative relationships.
- Clusters.
- Potential outliers.
- Distribution patterns.


## Identifying Outliers - Outlier detection
Outliers are observations that are unusually high or low compared with the rest of the dataset.

They may indicate unusual customer behaviour, data-entry errors or exceptional transactions.

## Boxplot - Outlier Detection in Field / Column Values

```
for column in ['Date', 'Product', 'Quantity', 'UnitPrice',
       'PaymentMethod', 'OrderStatus',
       'ItemsInCart', 'CouponCode', 'ReferralSource', 'TotalPrice']:
    plt.figure(figsize=(15, 4))
    sns.boxplot(data=DecodeLabs_df, x=column)
    plt.title(column)
    plt.show()
```

<img width="884" height="287" alt="image" src="https://github.com/user-attachments/assets/95a2141e-8c7b-4250-9526-77234ddc5968" />
<img width="884" height="282" alt="image" src="https://github.com/user-attachments/assets/2e5df348-1a50-44df-93aa-79d658135895" />
<img width="882" height="278" alt="image" src="https://github.com/user-attachments/assets/7fd39c48-916e-464a-ab27-50bc8a327c06" />
<img width="881" height="282" alt="image" src="https://github.com/user-attachments/assets/655b0833-3b2b-4011-814f-edf52aebd4e8" />
<img width="881" height="277" alt="image" src="https://github.com/user-attachments/assets/ddd6a81f-9c6b-491c-a37b-59a5dc3c144d" />
<img width="878" height="279" alt="image" src="https://github.com/user-attachments/assets/ec3d089f-0a50-4a9a-bf1b-8d777a87fc5f" />
<img width="881" height="286" alt="image" src="https://github.com/user-attachments/assets/509938e4-8fbe-4ab3-bd5b-b0f14bfa4237" />
<img width="878" height="281" alt="image" src="https://github.com/user-attachments/assets/41e77f79-c503-4480-a4ab-3af1b79bb960" />
<img width="881" height="282" alt="image" src="https://github.com/user-attachments/assets/0bcb5bec-a593-4e8b-acb3-c880155d7f7d" />
<img width="879" height="281" alt="image" src="https://github.com/user-attachments/assets/88f6a5d1-bfeb-4d5a-b516-4f9da599aea1" />


## Group By Analysis – Extracting Business Insights

### Product Performance Analysis
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
<img width="473" height="290" alt="image" src="https://github.com/user-attachments/assets/222744ad-f137-4031-ad9c-5a0e39e9bf28" />

## B. Interquartile Range (IQR) - Outlier Detection

```
Q1 = DecodeLabs_df['TotalPrice'].quantile(0.25)
Q3 = DecodeLabs_df['TotalPrice'].quantile(0.75)

IQR = Q3 - Q1

lower_limit = Q1 - 1.5 * IQR
upper_limit = Q3 + 1.5 * IQR

outliers = DecodeLabs_df[
    (DecodeLabs_df['TotalPrice'] < lower_limit) |
    (DecodeLabs_df['TotalPrice'] > upper_limit)
]

print('Number of outliers:', len(outliers))
print(outliers)
```
<img width="546" height="433" alt="image" src="https://github.com/user-attachments/assets/957a932a-20fd-4eb7-bb14-7b96f4eb4247" />






























































 
