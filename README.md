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
This project demonstrates the core analytical discipline behind effective EDA: inspect the data, test its quality, understand distributions, explore relationships, investigate outliers, analyse trends and translate the results into business-facing observations.

The central takeaway: meaningful analytics begins before the dashboard or model. It begins by asking better questions of the data and following the evidence wherever it leads.
Project notebook: DecodeLabs- Project 2 Python Final.ipynb
