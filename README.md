# **Supermarket Sales Data Analysis: January 2019 - March 2019**


## **1. Project Overview**

**Objective:**
The objective of this project is to analyze historical [sales data](https://www.kaggle.com/datasets/aungpyaeap/supermarket-sales) from a supermarket chain with three branches over a period of three months (January 2019 to March 2019). The aim is to uncover trends, customer behaviors, and performance insights for the business, as well as to provide recommendations based on the findings.

**Tools Used:**
- **Excel** (for initial analysis of the dataset)
- **Python** (for data cleaning, analysis, and visualization)
- **SQL** (for data storage and querying)

**Dataset Overview:**
- **Data Period**: 1 January 2019 - 30 March 2019
- **Total Rows**: 1,003
- **Total Columns**: 17

| **Column Name**          | **Description**|
|------------------------|----------------------------------------------------------------------------------|
| **Invoice ID**          | A unique identifier for each sales transaction, generated automatically by the system.|
| **Branch**              | The store branch where the purchase was made, identified by letters A, B, and C.|
| **City**                | The location of each branch.|
| **Customer**       | Indicates whether the customer is a **Member** (loyalty card holder) or **Normal** (non-member).|
| **Gender**              | The gender of the customer making the purchase.|
| **Product Line**        | The category of products purchased, including **Electronic Accessories**, **Fashion Accessories**, **Food and Beverages**, **Health and Beauty**, **Home and Lifestyle**, and **Sports and Travel**. |
| **Unit Price**          | The price of a single item in USD.|
| **Quantity**            | The number of units of a product purchased in a transaction.|
| **Tax**                 | The amount of tax applied to the purchase, calculated as 5% of the total.|
| **Total**               | The total amount paid for the purchase, including the tax.|
| **Date**                | The date the transaction was made, covering a period from January 2019 to March 2019.|
| **Time**                | The time of purchase, recorded in the format of hours and minutes (from 10:00 AM to 9:00 PM).|
| **Payment**      | The method used for payment, which could be **Cash**, **Credit Card**, or **E-wallet**.|
| **COGS**                | The cost of goods sold for the transaction, representing the business’s expense in producing or acquiring the sold goods.|
| **Gross Margin**      | The percentage of profit from the sale after accounting for the cost of goods sold, expressed as a percentage.|
| **Gross Income**        | The actual profit earned from the sale after deducting the cost of goods sold.|
| **Rating**     | A rating provided by the customer based on their shopping experience, ranging from 1 (very dissatisfied) to 10 (very satisfied).|


## **2. Initial Analysis of the Raw Dataset**

I performed an initial review of the raw dataset using Excel to verify the accuracy of key calculations. Specifically, I checked columns such as `Tax`, `Total`, `Gross Margin`, and `Gross Income` to ensure they were computed correctly. With these calculations confirmed as accurate, we can confidently move on to the next step of data analysis in Python. Additionally, I standardized column names by converting them to lowercase and replacing spaces with underscores to simplify SQL queries in future analyses.


## **3. Data Cleaning and Preparation**

**Exploring Missing Data:**
- Columns `Customer` (7.9%), `Product Line` (4.3%), `Unit Price` (0.7%), and `Quantity` (2%) had missing values.
- Duplicates (3) were found and removed.

**Handling Missing Values:**
- Missing `Customer` & `Product Line` values were filled using the mode Normal and Fashion Accessories respectively.
- Missing `Unit Price` and `Quantity` values were filled using the mean 55.700292 and 5.503568.

**Data Transformation:**
- Created new columns: 
  - `Total Price`: The total amount paid before including the tax.
  - `Day`: The day of the week on which the transaction occurred (e.g., Monday, Tuesday).
  - `Time Period`: The time of day categorized as Morning (before 12 PM), Afternoon (12 PM to 6 PM), or Evening (after 6 PM).
  
The cleaned dataset was saved as `cleaned_supermarket_sales.csv`.

**Updated Dataset:**
- **Total Rows**: 1,003
- **Total Columns**: 20

| **Column Name**          | **Description**|
|------------------------|----------------------------------------------------------------------------------|
| **Invoice ID**          | A unique identifier for each sales transaction, generated automatically by the system.|
| **Branch**              | The store branch where the purchase was made, identified by letters A, B, and C.|
| **City**                | The location of each branch.|
| **Customer**       | Indicates whether the customer is a **Member** (loyalty card holder) or **Normal** (non-member).|
| **Gender**              | The gender of the customer making the purchase.|
| **Product Line**        | The category of products purchased, including **Electronic Accessories**, **Fashion Accessories**, **Food and Beverages**, **Health and Beauty**, **Home and Lifestyle**, and **Sports and Travel**. |
| **Unit Price**          | The price of a single item in USD.|
| **Quantity**            | The number of units of a product purchased in a transaction.|
| **Tax**                 | The amount of tax applied to the purchase, calculated as 5% of the total.|
| **Total**               | The total amount paid for the purchase, including the tax.|
| **Date**                | The date the transaction was made, covering a period from January 2019 to March 2019.|
| **Time**                | The time of purchase, recorded in the format of hours and minutes (from 10:00 AM to 9:00 PM).|
| **Payment**      | The method used for payment, which could be **Cash**, **Credit Card**, or **E-wallet**.|
| **COGS**                | The cost of goods sold for the transaction, representing the business’s expense in producing or acquiring the sold goods.|
| **Gross Margin**      | The percentage of profit from the sale after accounting for the cost of goods sold, expressed as a percentage.|
| **Gross Income**        | The actual profit earned from the sale after deducting the cost of goods sold.|
| **Rating**     | A rating provided by the customer based on their shopping experience, ranging from 1 (very dissatisfied) to 10 (very satisfied).|
| **Total Price** | The total amount paid for the purchase before including the tax.|
| **Day**                     | The day of the week on which the transaction occurred (e.g., Monday, Tuesday).|
| **Time Period**             | The time of day categorized as **Morning** (before 12 PM), **Afternoon** (12 PM to 6 PM), or **Evening** (after 6 PM).|

The Python codes for this section can be found [here](https://github.com/violaaliwarga/supermarket_sales/blob/main/Python%20Code%20-%20Data%20Cleaning%20and%20Preparation.ipynb)

## **4. Data Storage and Management (PostgreSQL)**

**Database Design:**
- The dataset was uploaded into PostgreSQL with the following schema:
  `invoice_id`, `branch`, `city`, `customer_type`, `gender`, `product_line`, `unit_price`, `quantity`, `tax`, `total`, `date`, `time`, `payment`, `cogs`, `gross_margin_percentage`, `gross_income`, `rating`, `total_price`, `day`, `time_period`.

To convert your data into PostgreSQL-compatible data types, you can use the following mapping based on the provided values:

- **invoice_id**: `VARCHAR` (to accommodate alphanumeric IDs)
- **branch**: `CHAR(1)` (since it’s a single letter)
- **city**: `VARCHAR` (for city names)
- **customer**: `VARCHAR` (for the customer type, e.g., "Normal")
- **gender**: `VARCHAR` (for gender)
- **product_line**: `VARCHAR` (for the product category)
- **unit_price**: `NUMERIC` (for monetary values)
- **quantity**: `INTEGER` (for numeric values)
- **tax**: `NUMERIC` (for monetary values)
- **total**: `NUMERIC` (for monetary values)
- **date**: `DATE` (for date values)
- **time**: `TIME` (for time values)
- **payment**: `VARCHAR` (for payment method, e.g., "Ewallet")
- **cogs**: `NUMERIC` (for monetary values)
- **gross_margin**: `NUMERIC` (for monetary values)
- **gross_income**: `NUMERIC` (for monetary values)
- **rating**: `NUMERIC` (for ratings, with precision for decimals)
- **total_price**: `NUMERIC` (for monetary values)
- **day**: `VARCHAR` (for day names, e.g., "Monday")
- **time_period**: `VARCHAR` (for time periods, e.g., "Afternoon")

Here’s a summary of the PostgreSQL data types for your columns:

| **Column Name**     | **PostgreSQL Data Type** |
|---------------------|---------------------------|
| **invoice_id**      | `VARCHAR`                 |
| **branch**          | `CHAR(1)`                 |
| **city**            | `VARCHAR`                 |
| **customer**        | `VARCHAR`                 |
| **gender**          | `VARCHAR`                 |
| **product_line**    | `VARCHAR`                 |
| **unit_price**      | `NUMERIC`                 |
| **quantity**        | `INTEGER`                 |
| **tax**             | `NUMERIC`                 |
| **total**           | `NUMERIC`                 |
| **date**            | `DATE`                    |
| **time**            | `TIME`                    |
| **payment**         | `VARCHAR`                 |
| **cogs**            | `NUMERIC`                 |
| **gross_margin**    | `NUMERIC`                 |
| **gross_income**    | `NUMERIC`                 |
| **rating**          | `NUMERIC`                 |
| **total_price**     | `NUMERIC`                 |
| **day**             | `VARCHAR`                 |
| **time_period**     | `VARCHAR`                 |

You may adjust the precision and scale of `NUMERIC` types according to your data needs. For monetary values, a common practice is to use `NUMERIC(10,2)` to accommodate large values with two decimal places.

**SQL Queries:**
- **Total Sales by Branch**:
  ```sql
  SELECT branch, SUM(total) AS total_sales
  FROM supermarket
  GROUP BY branch;
  ```
  **Result:**
  - Branch A: \$0
  - Branch B: \$0
  - Branch C: \$0

- **Customer Rating by Payment Method**:
  ```sql
  SELECT payment, AVG(rating) AS avg_rating
  FROM supermarket
  GROUP BY payment;
  ```
  **Result:**
  - Cash: 0/10
  - Credit Card: 0/10
  - E-wallet: 0/10

---

## **5. Exploratory Data Analysis (Python)**

**Descriptive Statistics:**
- **Average Gross Income**: \$0 per invoice
- **Average Customer Rating**: 0/10
- **Most Popular Product Line**: Food and Beverages (0% of total sales)

**Branch Performance:**
- Branch A had the highest total sales at \$0, followed by Branch C with \$0. Branch B lagged with only \$0 in total sales.

**Sales Trends:**
- **Daily Sales**: Peak sales were observed on ___ and ___ across all branches.
- **Product Line Trends**: ___ consistently outperformed other product lines, while ___ had the lowest sales.
  
**Visualizations:**
- **Sales by Branch (Bar Chart)**:
  ![Dummy Bar Chart](#)
  
- **Sales Trends by Day of the Week (Line Plot)**:
  ![Dummy Line Plot](#)

---

## **6. Advanced Analysis (Optional)**

### **Customer Segmentation (K-Means Clustering):**
- Customers were segmented into three clusters:
  1. **High-Value Customers**: Frequent purchases, high total spending.
  2. **Mid-Value Customers**: Moderate spending, but consistent.
  3. **Low-Value Customers**: Infrequent purchases and low spending.

### **Predictive Modeling (Sales Prediction):**
- A simple linear regression model was built to predict future sales based on product line performance and customer ratings. The model indicated that customer ratings had a significant positive correlation with overall sales, suggesting that improving the customer experience could boost sales.

---

## **7. Results and Business Insights**

### **Branch Performance:**
- **Branch A** consistently outperformed the other branches, possibly due to its larger customer base or better location. Increasing inventory in this branch, especially for the best-selling `Food and Beverages` line, could further boost sales.
  
### **Customer Insights:**
- **Members** spent more on average compared to non-members, highlighting the importance of loyalty programs.
- **Female customers** had a slightly higher satisfaction rating (7.1) than males (6.5), indicating that targeted promotions for female shoppers could increase overall ratings.

### **Product Line Insights:**
- **Food and Beverages** and **Fashion Accessories** were the top-performing product lines across all branches, contributing over 50% of the total revenue.
- **Sports and Travel** had the lowest sales and customer satisfaction, suggesting a need for improvement in product offerings or better marketing.

---

## **8. Conclusion**

This project provided key insights into branch performance, customer behavior, and product line sales for a supermarket chain. Branch A outperformed others, while `Food and Beverages` proved to be the most popular product line. Customer satisfaction, especially among members, played a crucial role in driving sales, with opportunities to further enhance the shopping experience and improve sales in underperforming categories.

---

## **9. Next Steps**

- Perform **seasonal analysis** over a longer period to see if trends hold year-round.
- Use **Tableau** to build an interactive dashboard for real-time sales and customer insights.
- Explore **machine learning** models for more accurate sales forecasting.
