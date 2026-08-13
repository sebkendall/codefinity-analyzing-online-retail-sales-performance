-e This file is a merged representation of the entire codebase, combined into a single document

## Purpose
This file contains a packed representation of the entire repository's contents.
It is designed to be easily consumable by AI systems for analysis, code review,
or other automated processes.

## File Format
The content is organized as follows:
1. This summary section
2. Repository information
3. Directory structure
4. Multiple file entries, each consisting of:
  a. A header with the file path (## File: path/to/file)
  b. The full contents of the file in a code block or first three lines for files with .csv extensions

## Usage Guidelines
- This file should be treated as read-only. Any changes should be made to the
  original repository files, not this packed version.
- When processing this file, use the file path to distinguish
  between different files in the repository.
- Be aware that this file may contain sensitive information. Handle it with
  the same level of security as you would the original repository.

## Notes
- This file includes only .ipynb and .csv file contents in full or partial form
- All other file types are represented only through the directory structure
- Binary files are not included in this packed representation. Please refer to the Repository Structure section for a complete list of file paths, including binary files

# Directory Structure

````
./
fs_report.md
main.py
online_retail.csv
````
-e 
# Files
-e 
## File: online_retail.csv
````
,InvoiceNo,StockCode,Description,Quantity,InvoiceDate,UnitPrice,CustomerID,Country
0,536370,22728,ALARM CLOCK BAKELIKE PINK,24,01.12.2010 08:45,3.75,12583.0,France
1,536370,22727,ALARM CLOCK BAKELIKE RED ,24,01.12.2010 08:45,3.75,12583.0,France
````
-e 
## File: main.py
````
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load subset for performance
df = pd.read_csv("online_retail.csv")
print(df.head())

# Your code starts here

# Task 1
df['Revenue'] = df['Quantity'] * df['UnitPrice']
revenue_by_country = df.groupby('Country', as_index=False)['Revenue'].sum()
ranked_revenues = revenue_by_country.sort_values(by='Revenue', ascending=False)
print(f'\nTotal revenue by country: \n{ranked_revenues}\n') 

plt.figure(figsize=(10, 8))
sns.barplot(data=ranked_revenues, x='Revenue', y='Country')
plt.title('Total Revenue by Country')
plt.xlabel('Total Revenue')
plt.ylabel('Country')
plt.tight_layout()
plt.show()

# Task 2
purchased_products = df.groupby('Description', as_index=False)['Quantity'].sum()
most_purchased = purchased_products.sort_values(by='Quantity', ascending=False).head(10)
print(f'\nThe top 10 most frequently purchased products are: \n{most_purchased}')

# Task 3
df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'], dayfirst=True, format='%d.%m.%Y %H:%M')

df['InvoiceMonth'] = df['InvoiceDate'].dt.month
df['InvoiceYear'] = df['InvoiceDate'].dt.year
print( '\n', df[['InvoiceDate', 'InvoiceMonth', 'InvoiceYear']].head())

df['InvoiceMonthName'] = df['InvoiceDate'].dt.month_name()

monthly_revenue = df.groupby('InvoiceMonthName', as_index=False)['Revenue'].sum()

month_order = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']

monthly_revenue['InvoiceMonthName'] = pd.Categorical(monthly_revenue['InvoiceMonthName'], categories=month_order, ordered=True)

ord_month_revs = monthly_revenue.sort_values('InvoiceMonthName')
print(f'\nTotal revenue per month: \n{ord_month_revs}\n')

plt.figure(figsize=(10,6))
sns.barplot(data=ord_month_revs, x='InvoiceMonthName', y='Revenue')
plt.title('Total Revenue per Month')
plt.xlabel('Month')
plt.ylabel('Total Revenue')
plt.tight_layout()
plt.show()

# Task 4
order_values = df.groupby('InvoiceNo', as_index=False)['Revenue'].sum()

customer_invoices = df[['InvoiceNo', 'CustomerID']].drop_duplicates()
customer_orders = pd.merge(order_values, customer_invoices, on='InvoiceNo')

avg_order_value = customer_orders.groupby('CustomerID', as_index=False)['Revenue'].mean().rename(columns={'Revenue': 'AverageOrderValue'})

print(f'\nAverage Order Value per Customer: \n{avg_order_value.head()}')

# Task 5
order_items = df.groupby(['InvoiceNo', 'Country'], as_index=False)['Quantity'].sum()

order_items['LargeOrder'] = order_items['Quantity'] > 10

country_order_counts = order_items.groupby('Country')['InvoiceNo'].count().rename('TotalOrders')
country_large_counts = order_items[order_items['LargeOrder']].groupby('Country')['InvoiceNo'].count().rename('LargeOrders')

order_proportion = pd.concat([country_order_counts, country_large_counts], axis=1).fillna(0)
order_proportion['LargeProportionOrders'] = (order_proportion['LargeOrders'] / order_proportion['TotalOrders']) * 100
order_proportion = order_proportion.reset_index()

print(f'\nProportion of orders with more than 10 items by Country (%):')
print(order_proportion[['Country', 'LargeProportionOrders']])

# Task 6
customer_total_spend = df.groupby('CustomerID', as_index=False)['Revenue'].sum()
ranked_customers = customer_total_spend.sort_values(by='Revenue', ascending=False).head()

print(f'\nThe top 5 customers total spend are: \n{ranked_customers}')








````
