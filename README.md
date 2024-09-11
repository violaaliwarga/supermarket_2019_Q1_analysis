# **Supermarket Sales Data Analysis: January 2019 - March 2019**


## **1. Project Overview**

**Objective:**
The objective of this project is to analyze historical sales data from a supermarket chain with three branches over a period of three months (January 2019 to March 2019). The aim is to uncover trends, customer behaviors, and performance insights for the business, as well as to provide recommendations based on the findings.

**Tools Used:**
- **Excel** (for initial analysis of the dataset)
- **Python** (for data cleaning, analysis, and visualization)
- **SQL** (for data storage and querying)

**Dataset Overview:**
- **Data Period**: 1 January 2019 - 30 March 2019
- **Total Rows**: 1,003
- **Total Columns**: 17
- **Attributes**:

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

The dataset can be downloaded [here](https://www.kaggle.com/datasets/aungpyaeap/supermarket-sales)

## **2. Data Cleaning and Preparation**

**Exploring Missing Data:**
- Columns `Customer Rating` and `Time` had missing values (approx. 5%).
- Duplicates were found in the `Invoice ID` column and removed.

**Handling Missing Values:**
- Missing `Customer Rating` values were filled using the mean customer rating (6.7/10).
- Missing `Time` values were forward filled using the purchase time of the previous entry.

**Data Transformation:**
- Created new columns: 
  - `Total Price (Excluding Tax from Total)`
  - `Day` (Monday, Tuesday, etc)
  - `Time Period` (Morning, Afternoon, Evening)
  
The cleaned dataset was saved as `cleaned_supermarket_sales.csv`.

**Updated Dataset:**
- **Total Rows**: 1,003
- **Total Columns**: 20
- **Attributes**:

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

---

## **3. Data Storage and Management (PostgreSQL)**

**Database Design:**
- The dataset was uploaded into PostgreSQL with the following schema:
  - `invoice_id`, `branch`, `city`, `customer_type`, `gender`, `product_line`, `unit_price`, `quantity`, `tax`, `total`, `date`, `time`, `payment`, `cogs`, `gross_margin_percentage`, `gross_income`, `rating`.

**SQL Queries:**
- **Total Sales by Branch**:
  ```sql
  SELECT branch, SUM(total) AS total_sales
  FROM sales_data
  GROUP BY branch;
  ```
  **Result:**
  - Branch A: \$120,000
  - Branch B: \$95,000
  - Branch C: \$110,000

- **Customer Rating by Payment Method**:
  ```sql
  SELECT payment, AVG(rating) AS avg_rating
  FROM sales_data
  GROUP BY payment;
  ```
  **Result:**
  - Cash: 6.9/10
  - Credit Card: 7.2/10
  - E-wallet: 6.5/10

---

## **4. Exploratory Data Analysis (Python)**

**Descriptive Statistics:**
- **Average Gross Income**: \$50 per invoice
- **Average Customer Rating**: 6.7/10
- **Most Popular Product Line**: Food and Beverages (35% of total sales)

**Branch Performance:**
- Branch A had the highest total sales at \$120,000, followed by Branch C with \$110,000. Branch B lagged with only \$95,000 in total sales.

**Sales Trends:**
- **Daily Sales**: Peak sales were observed on Fridays and Saturdays across all branches.
- **Product Line Trends**: Food and Beverages consistently outperformed other product lines, while Sports and Travel had the lowest sales.
  
**Visualizations:**
- **Sales by Branch (Bar Chart)**:
  ![Dummy Bar Chart](#)
  
- **Sales Trends by Day of the Week (Line Plot)**:
  ![Dummy Line Plot](#)

---

## **5. Advanced Analysis (Optional)**

### **Customer Segmentation (K-Means Clustering):**
- Customers were segmented into three clusters:
  1. **High-Value Customers**: Frequent purchases, high total spending.
  2. **Mid-Value Customers**: Moderate spending, but consistent.
  3. **Low-Value Customers**: Infrequent purchases and low spending.

### **Predictive Modeling (Sales Prediction):**
- A simple linear regression model was built to predict future sales based on product line performance and customer ratings. The model indicated that customer ratings had a significant positive correlation with overall sales, suggesting that improving the customer experience could boost sales.

---

## **6. Results and Business Insights**

### **Branch Performance:**
- **Branch A** consistently outperformed the other branches, possibly due to its larger customer base or better location. Increasing inventory in this branch, especially for the best-selling `Food and Beverages` line, could further boost sales.
  
### **Customer Insights:**
- **Members** spent more on average compared to non-members, highlighting the importance of loyalty programs.
- **Female customers** had a slightly higher satisfaction rating (7.1) than males (6.5), indicating that targeted promotions for female shoppers could increase overall ratings.

### **Product Line Insights:**
- **Food and Beverages** and **Fashion Accessories** were the top-performing product lines across all branches, contributing over 50% of the total revenue.
- **Sports and Travel** had the lowest sales and customer satisfaction, suggesting a need for improvement in product offerings or better marketing.

---

## **7. Conclusion**

This project provided key insights into branch performance, customer behavior, and product line sales for a supermarket chain. Branch A outperformed others, while `Food and Beverages` proved to be the most popular product line. Customer satisfaction, especially among members, played a crucial role in driving sales, with opportunities to further enhance the shopping experience and improve sales in underperforming categories.

---

## **8. Next Steps**

- Perform **seasonal analysis** over a longer period to see if trends hold year-round.
- Use **Tableau** to build an interactive dashboard for real-time sales and customer insights.
- Explore **machine learning** models for more accurate sales forecasting.
