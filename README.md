# Total Revenue by Country plot
Multiplied Quantity by UnitPrice for each invoice line to get its revenue.
Grouped all rows by Country and sums their Revenue.
Printed the DataFrame of countries with their total revenues from highest to lowest.
Uses Seaborn’s barplot to draw a horizontal bar chart showing revenue per country in this order.

# Top 10 Most Frequently Purchased Products
Totaled how many units of each product description were sold.
Sorted quantity in descending order and kept the first ten.

# Seasonal Trends (Monthly Revenue)
Parsed the date/time strings into pandas timestamps.
Created new columns for numeric month, year, and the month’s name.
Summed the Revenue for each calendar month (by name).
Ensured the month names sort in calendar order rather than alphabetically.
Printed the monthly revenue table and used a bar chart to show monthly totals.

# Average Order Value per Customer
Aggregated revenue by invoice number.
Kept one row per invoice-customer pair, then joins with invoice totals.
Calculated the mean revenue across all invoices for each customer.
Showed each customer’s average order value.

# Proportion of “Large” Orders per Country
Totaled the number of items on each invoice, with its country.
Marked invoices that contain more than ten items.
Created one series for total orders and one for orders flagged as large.
Divided  large-order count by total orders, then multiplied by 100.
Displayed each country’s percentage of orders that are “large.”

# Top 5 Customers by Total Spend
Aggregated each customer’s total spend across all invoices.
Sorted customers by spend and picked the top five.
Showed those five IDs with their total revenues.








