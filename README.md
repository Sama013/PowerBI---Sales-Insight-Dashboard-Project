# Sales Insights Dashboard Project

## Problem Statement

Atliq Hardware supplies computer hardware and peripherals to clients across India. The market is growing dynamically, and the Sales Director, Bhavin Patel, faces challenges in tracking sales in this rapidly evolving market. He is struggling to obtain clear and actionable insights into his business operations. The regional managers from North, South, and Central India provide quarterly sales updates over the phone, which are neither reliable nor accurate. 

Bhavin has noticed a drop in sales, but the regional managers insist that sales remain profitable. They send multiple Excel files as proof, which require significant time and effort to interpret. This approach results in unreliable insights and discrepancies in sales reporting, making it difficult for Bhavin to get a clear, accurate picture of the company's performance.

Bhavin is seeking a more efficient and transparent method to gain insights into the company's sales data. He desires simple, understandable insights through a visual dashboard that he can access daily. Additionally, he wants an email notification system where Power BI sends him a monthly overview of the numbers and the overall business performance in terms of revenue. This solution will enable Bhavin to bypass the regional managers' inconsistent updates and, instead of relying on phone calls, obtain precise and truthful insights through Power BI. This, in turn, will empower him to make informed, data-driven decisions, enhancing the overall efficiency and effectiveness of the company's sales tracking and reporting processes.

## Project Planning

### AIMS Grid

- **Purpose**: To unlock hidden sales opportunities for the sales teams, enhance decision-making support, and automate processes to significantly reduce the manual time spent on gathering data.
- **Stakeholders**: Sales Director, Marketing Team, Customer Service Team, Data & Analytics Team, IT
- **Result**: An automated dashboard providing real-time information and quick, up-to-date sales insights to support data-driven decision-making.

### Success Criteria

1. **Accurate Sales Tracking**:
   - Eliminate discrepancies or inconsistencies in sales reporting.
   - Implement a system with a visual Power BI dashboard that provides real-time, accurate sales data for all regions (North, South, and Central India) in an easily understandable format.

2. **Automated Reporting**:
   - Sales analysts stop gathering data manually, saving 20% of their business time and reinvesting it in value-added activities.
   - Establish an automated email notification system to update the sales director with a monthly overview of sales and revenue performance.

3. **Enhanced Decision-Making**:
   - Decrease reliance on regional managers for sales updates, resulting in more accurate data.
   - Provide reliable and actionable insights through the Power BI dashboard, enabling Bhavin Patel to make informed, data-driven decisions.

4. **Improved Sales Performance**:
   - Sales analysts stop gathering data manually to save 20% of their business time and reinvest it in value-added activities.

## Data Discovery and Integration

During the data discovery phase, the data analyst team collaborates with the IT team, which owns the software system that tracks sales records. These records are stored in a MySQL database. Power BI is connected to this database to pull the necessary information required for data analysis.

## Data Analysis Using SQL

Here are some SQL queries used to analyze the sales data:

1. Show all customer records:

   SELECT * FROM customers;
2. Show total number of customers
   
    `SELECT count(*) FROM customers;`
3. Show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`
4. Show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`
5. Show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD"`
6. Show transactions in 2020 join by date table

     `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`
7. Show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

8. Show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
and transactions.market_code="Mark001";`

Data Analysis Using Power BI
============================

1. Formula to create norm_amount column

`= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)`
