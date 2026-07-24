# ***ElectroHub Power BI Dashboard***

***Overview***
This project presents an interactive Power BI dashboard for ElectroHub, built from a retail sales dataset containing customer, product, promotion, and transactional order data across multiple categories including Electronics, Footwear, Clothing, Home Appliances, Accessories, Kitchenware, Bags, and Personal Care.

The dashboard was designed to answer the stated business questions around top and bottom product performance, sales trends over time, the relationship between sales and profit, period-over-period comparisons, discount analysis, order-level drilldown, and city-level sales analysis.

***Dataset***
The Excel workbook contains a dimensional retail model with separate sheets for customers, products, promotions, and order transactions.

***Source tables***
Dim Customers: customer master data with Customer ID, name, city, state, pincode, email, and phone number.

Dim Product: product master with Product ID, product name, product line, and price in INR.

Dim Promotion: promotion details with Promotion ID, promotion name, ad type, coupon code, and price reduction type.

Transactions sheet: order-level records with order date, customer ID, promotion ID, product ID, units sold, price per unit, total sales, discount percentage, discount value, and net sales.

***Business requirements addressed:***
The dashboard was built to satisfy the following reporting requirements:

Top and bottom 5 products by Sales, Profit, and Quantity Sold.

Sales trends by day, month, quarter, and year.

Relationship between Sales and Profit.

Comparison of Sales, Profit, and Quantity Sold between any two user-selected periods.

Average discount by discount category.

Total number of orders.

Order-level detail view with Sales, Profit, Discount, Net Sales, and filterable fields.

Sales by city.

***Dashboard build process***
The dashboard creation followed a structured workflow from raw data preparation to report design.

***1. Data import***
Imported the Excel workbook into Power BI Desktop.

Loaded the customer, product, promotion, and transaction sheets into Power Query for validation and modeling.

***2. Data cleaning and preparation***
Verified data types for date, numeric, and text columns so aggregations and time intelligence would work correctly.

Standardized key fields such as Customer ID, Product ID, and PromotionID to support relationships across tables.

Reviewed null or incomplete numeric fields in the transaction sheet and prepared calculated fields in the model where needed for analysis such as Sales, Discount, Net Sales, and Profit.

***3. Data modeling***
Built relationships between the transaction table and the customer, product, and promotion dimension tables using their respective keys.

Used a star-schema style model so slicers and cross-filtering would behave consistently across visuals.

Connected city and state analysis through the customer dimension because location attributes are stored in Dim Customers.

***4. Calculations and measures***
The model supports the core business KPIs and analysis requirements using calculated columns and measures derived from the available fields in the dataset.

***Typical Power BI measures used in the dashboard include:***

text
Total Sales = SUM('Orders'[Total Sales])
Total Discount = SUM('Orders'[Discount Value])
Net Sales = SUM('Orders'[Net Sales])
Total Orders = COUNTROWS('Orders')
Quantity Sold = SUM('Orders'[Units Sold])
Profit = [Net Sales] - SUMX('Orders', 'Orders'[Units Sold] * RELATED('Dim Product'[Price (INR)]))
A proper date table can also be created to support daily, monthly, quarterly, and annual trend reporting:
text
Date Table = CALENDAR(MIN('Orders'[Date (dd/mm/yyyy)]), MAX('Orders'[Date (dd/mm/yyyy)]))

***5. Report design***
The report layout was organized to match the analytical questions in the requirement file.

***Suggested page structure:***

***Executive overview:*** KPI cards for Total Sales, Profit, Net Sales, Quantity Sold, Average Discount, and Total Orders.

***Product performance:*** Top 5 and Bottom 5 products by Sales, Profit, and Quantity Sold using bar charts.

***Time trends:*** line or area charts showing daily, monthly, quarterly, and annual sales movement.

***Sales vs Profit:*** scatter chart to show the relationship between revenue and profitability.

***Period comparison:*** slicer-driven comparison view for two selected periods.

***Discount analysis:*** a chart showing the average discount by discount category or promotion type.

***Geography analysis:*** map chart of sales by city using the customer table location fields.

***Order details:*** table containing Sales, Profit, Discount, Net Sales, Product, Date, Customer ID, and Promotion filters.

***6. Interactivity***
Added slicers for Product, Date, Customer Name, and Promotion Category as specifically requested in the business requirements.

Enabled cross-filtering so users could move from summary KPIs to detailed transactional views.

Used visual-level filters where appropriate for Top N and Bottom N product analysis.

***7. Formatting and usability***
Applied consistent titles, category labels, and number formatting for INR-based metrics and counts.

Used business-friendly visual grouping so stakeholders can move from overview to drilldown quickly.

Kept the order detail table filterable to support operational review of individual transactions.

***Key insights supported by the dashboard***
The final dashboard enables stakeholders to answer the following questions directly:

Which products are the best and worst performers by sales, profit, and quantity sold?

How does sales performance change across different time levels?

Are high-sales products also high-profit products?

How do two selected business periods compare?

Which promotions or discount bands drive larger average discounts?

Which cities contribute the most sales?

What does each individual order contribute in terms of sales, discount, and net sales?

****Repository contents***
A complete GitHub repository for this project includes:

Store-Data.xlsx — raw dataset.

ElectroHub Dashboard.pbix — Power BI report file.

Power-BI-Project-1-Requirements.pptx - PowerPoint file highlighting the business requirements.

README.md — project documentation.

Dashboard screenshots

<img width="2560" height="1392" alt="Overview" src="https://github.com/user-attachments/assets/f0a8d711-d218-44fa-bb59-a254da34497e" />

<img width="2560" height="1392" alt="TopBottom-Analysis" src="https://github.com/user-attachments/assets/c7dbd511-8e6a-4482-816f-fcaa5e969b12" />

<img width="2560" height="1392" alt="Comparision Sales-Profit-QTY" src="https://github.com/user-attachments/assets/58f625aa-2ae9-476c-8539-3ba5bbdb09bc" />

<img width="2560" height="1392" alt="Edit-Interactions" src="https://github.com/user-attachments/assets/564fff94-b1fa-4d9e-ba28-d1f558634003" />

<img width="2560" height="1392" alt="Table-Visual" src="https://github.com/user-attachments/assets/759827f3-45ad-4db3-b12a-3fb6dcb15364" />

***Tools used***
Microsoft Excel for source data storage.

Power BI Desktop for data modeling, DAX calculations, visual design, and dashboard creation.

***Reproducibility steps***
To recreate the dashboard:

Open Power BI Desktop and import Store-Data.xlsx.

Load all sheets into the data model.

Clean column types and validate key relationships between transactions, customers, products, and promotions.

Create calculated measures for Sales, Profit, Discount, Net Sales, Orders, and Quantity Sold.

Build visuals aligned to the eight business requirements from the presentation.

Add slicers for Product, Date, Customer ID, and Promotion Category.

Format the report, validate interactions, and publish or export screenshots for GitHub.
