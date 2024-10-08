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
- **Total Rows**: 1,000
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

The dataset was uploaded into PostgreSQL with the following schema:

| **Column Name**     | **PostgreSQL Data Type** |
|---------------------|---------------------------|
| **invoice_id**      | `VARCHAR`                 |
| **branch**          | `CHAR(1)`                 |
| **city**            | `VARCHAR`                 |
| **customer**        | `VARCHAR`                 |
| **gender**          | `VARCHAR`                 |
| **product_line**    | `VARCHAR`                 |
| **unit_price**      | `NUMERIC`                 |
| **quantity**        | `NUMERIC`                 |
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


**SQL Queries:**
- **Average Gross Income**:
  ```sql
  SELECT AVG(gross_income) AS avg_gross_income
  FROM supermarket;
  ```
  **Result:**
  15.3793690000000000

- **Average Customer Rating**
  ```sql
  SELECT AVG(rating) AS average_customer_rating
  FROM supermarket;
  ```
  **Result:**
  6.9727000000000000

- **Total Sales by Product Line & Percentage from Total Sales**:
  ```sql
  SELECT product_line, SUM(total) AS total_sales
  FROM supermarket
  GROUP BY product_line
  ORDER BY total_sales DESC;;
  ```
  **Result:**
  - Fashion Accessories: \$64,571, 20%
  - Sports and Travel: \$53,970, 17%
  - Food and Beverages: \$52,923, 16%
  - Electronic Accessories: \$52,038, 16%
  - Home and Lifestyle: \$51,793, 16%
  - Health and Beauty: \$47,671, 15%

- **Total Sales by Branch**:
  ```sql
  SELECT branch, SUM(total) AS total_sales
  FROM supermarket
  GROUP BY branch;
  ```
  **Result:**
  - Branch A: \$106,200
  - Branch B: \$106,197
  - Branch C: \$110,568

- **Total Sales by Day**:
  ```sql
  SELECT day, SUM(total) AS total_sales
  FROM supermarket
  GROUP BY day;
  ```
  **Result:**
  - Monday: \$37,899
  - Tuesday: \$51,482
  - Wednesday: \$43,731
  - Thursday: \$45,349
  - Friday: \$43,926
  - Saturday: \$56,121
  - Sunday: \$44,458

- **Total Sales by Time Period**:
  ```sql
  SELECT time_period, SUM(total) AS total_sales
  FROM supermarket
  GROUP BY time_period
  ORDER BY time_period;
  ```
  **Result:**
  - Morning: \$61,799
  - Afternoon: \$172,469
  - Evening: \$88,699

- **Customer Rating by Payment Method**:
  ```sql
  SELECT payment, AVG(rating) AS avg_rating
  FROM supermarket
  GROUP BY payment;
  ```
  **Result:**
  - Cash: 6.97/10
  - Credit Card: 7/10
  - E-wallet: 6.95/10
 

## **5. Exploratory Data Analysis**

**Descriptive Statistics:**
- **Average Gross Income**: **\$15.38** per invoice
- **Average Customer Rating**: **7/10**
- **Most Popular Product Line**: **Fashion Accessories** (**20%** of total sales)

**Branch Performance:**
- **Branch C** had the highest total sales at **\$110,568**, followed by **Branch A** with **\$106,200**. Lastly, **Branch B** with **\$106,197** in total sales.

**Sales Trends:**
- **Daily Sales**: Peak sales were observed on **Saturday** and **Tuesday** across all branches. Also sales are higher in the **Afternoon** and least in the **Morning**
- **Product Line Trends**: **Fashion Accessories** consistently outperformed other product lines, while **Health and Beauty** had the lowest sales.
  
**Visualizations:**

<img src="https://github.com/user-attachments/assets/e849be8f-7208-4056-b8e7-f343ea2a483a" width="500">
<img src="https://github.com/user-attachments/assets/646cf280-ab2b-4236-9bc2-5021900bc497" width="500">
<br>
<br>
<br>
<img src="https://github.com/user-attachments/assets/da61e30c-54c1-43a6-822c-14a4eb7ed138" width="500">
<img src="https://github.com/user-attachments/assets/6b4ad774-b48d-47aa-8e2c-b09b02d33b67" width="500">
<br>
<br>
<br>
<img src="https://github.com/user-attachments/assets/029bbddd-cc03-42a6-8b5e-7640e7b0d5ad" width="500">
<img src="https://github.com/user-attachments/assets/1a9d9436-1290-472e-a6c7-e02ea10bbde6" width="300">
<br>
<br>
The Python codes for this section can be found [here](https://github.com/violaaliwarga/supermarket_sales/blob/main/Python%20Code%20-%20EDA%20Visualization.ipynb)


## **6. Advanced Analysis - Customer Segmentation (K-Means Clustering)**

Customers were segmented into three clusters:
1. **High-Value Customers**: Frequent purchases, high total spending.
2. **Mid-Value Customers**: Moderate spending, but consistent.
3. **Low-Value Customers**: Infrequent purchases and low spending.

### **6.1. Result**
  
  We have got three clusters (0, 1, and 2) with the following characteristics:

  **<ins>Cluster 0</ins>**
  - **Average Total Spent:** \$135.24
  - **Total Spent:** \$71,544.43
  - **Average Quantity:** 3.90 units
  - **Average Frequency:** 505.42 purchases

  **<ins>Cluster 1</ins>**
  - **Average Total Spent:** \$760.69
  - **Total Spent:** \$127,796.00
  - **Average Quantity:** 8.64 units
  - **Average Frequency:** 502.24 purchases

  **<ins>Cluster 2</ins>**
  - **Average Total Spent:** \$408.01
  - **Total Spent:** \$123,626.32
  - **Average Quantity:** 6.56 units
  - **Average Frequency:** 503.88 purchases

### 6.2. **Interpretation**

  **6.2.1. High-Value Customers (Cluster 1):**
  - **Average Total Spent:** \$760.69
  - **Average Quantity:** 8.64 units
  - **Total Spent:** \$127,796.00
  - **Average Frequency:** 502.24 purchases
  - **Characteristics of High-Value Customers:**
    - These customers spend significantly more per transaction compared to the other clusters.
    - They make a considerable number of purchases and buy more items per transaction.
    - This cluster represents high-value customers who contribute substantially to total revenue.

  **6.2.2. Mid-Value Customers (Cluster 2):**
  - **Average Total Spent:** \$408.01
  - **Average Quantity:** 6.56 units
  - **Total Spent:** \$123,626.32
  - **Average Frequency:** 503.88 purchases
  - **Characteristics of Mid-Value Customers:**
    - These customers spend moderately per transaction and buy a reasonable number of items.
    - They have a total spend and average quantity between the high-value and low-value clusters.
    - They are consistent but not as high-spending as Cluster 1.

  **6.2.3. Low-Value Customers (Cluster 0):**
  - **Average Total Spent:** \$135.24
  - **Average Quantity:** 3.90 units
  - **Total Spent:** \$71,544.43
  - **Average Frequency:** 505.42 purchases
  - **Characteristics of Low-Value Customers:**
    - These customers spend the least per transaction and buy fewer items.
    - They still contribute to a significant portion of total transactions but with lower spend per purchase.
    - They are infrequent or low-spending customers, contributing the least to total revenue.

### 6.3. **Summary**

- **Cluster 1** represents high-value customers who are frequent and spend significantly more per transaction.
- **Cluster 2** represents mid-value customers who spend and purchase moderately.
- **Cluster 0** represents low-value customers who spend the least per transaction and purchase fewer items.

### 6.4. **Actions and Strategy**

- **High-Value Customers:** Focus on retaining and rewarding these customers with loyalty programs, exclusive offers, and personalized marketing.
- **Mid-Value Customers:** Encourage increased spending through targeted promotions and upselling.
- **Low-Value Customers:** Improve engagement through incentives, discounts, or improved customer service to increase their spending.

The Python codes for this section can be found [here](https://github.com/violaaliwarga/supermarket_sales/blob/main/Python%20Code%20-%20Customer%20Segmentation.ipynb)


## **7. Results and Business Insights**

### **7.1. Overall Sales Performance**
- **Total Sales:** The total sales amount across all branches and product lines highlights the strong performance of the supermarket chain, with consistent sales across different branches. Branch C led in total sales, followed closely by Branches A and B.
- **Sales by Product Line:** Fashion Accessories emerged as the top-performing category, contributing significantly to total sales. Conversely, Health and Beauty had the lowest sales, suggesting potential areas for improvement or marketing focus.
- **Sales Trends:** Sales are highest on Saturdays and Tuesdays, and the Afternoon period sees the highest revenue, indicating peak shopping times for the supermarket. This insight could guide staffing and promotional strategies.

### **7.2. Customer Behavior**
- **Average Customer Rating:** The average rating of 7/10 reflects generally positive customer satisfaction. The slight variation in ratings based on payment methods suggests that customer experience may differ depending on payment options.
- **Customer Segmentation:** The K-Means clustering identified distinct customer segments:
  - **High-Value Customers:** Significant contributors to revenue; focus on retention strategies and exclusive offers.
  - **Mid-Value Customers:** Consistent spenders; potential for increased engagement through targeted promotions.
  - **Low-Value Customers:** Lower spenders; opportunities for improvement through incentives or enhanced service.

### **7.3. Recommendations**
- **Branch Performance:** Allocate resources and marketing efforts based on branch performance. Branch C's success could be analyzed for best practices and applied to other branches.
- **Product Line Strategies:** Enhance marketing efforts for underperforming product lines such as Health and Beauty, while capitalizing on the popularity of Fashion Accessories.
- **Sales Timing:** Optimize staffing and promotional activities during peak sales periods (Afternoon and weekends) to maximize revenue and customer satisfaction.

## **8. Conclusion**

The analysis of the supermarket sales data from January 2019 to March 2019 provides valuable insights into sales performance, customer behavior, and product line effectiveness. Key findings include:
- **Branch C** outperformed other branches in total sales.
- **Fashion Accessories** consistently led in sales, while **Health and Beauty** lagged behind.
- Peak sales occur on Saturdays and in the Afternoon.
- Customer segmentation revealed high-value, mid-value, and low-value customer groups, each requiring tailored strategies.

These insights offer actionable recommendations for improving sales strategies, customer engagement, and operational efficiency. By focusing on high-value customers, optimizing product lines, and adjusting staffing and promotional activities based on sales trends, the supermarket chain can enhance overall performance and customer satisfaction.
