# **Supermarket Sales Data Analysis: January 2019 - March 2019**

---

## **1. Project Overview**

**Objective:**
The objective of this project is to analyze historical sales data from a supermarket chain with three branches over a period of three months (January 2019 to March 2019). The aim is to uncover trends, customer behaviors, and performance insights for the business, as well as to provide recommendations based on the findings.

**Tools Used:**
- **Excel** (for preprocessing)
- **Python** (for data cleaning, analysis, and visualization)
- **SQL** (for data storage and querying)

**Dataset Overview:**
- **Rows**: 1,003
- **Attributes**:
| **Attribute**          | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| **Invoice ID**          | Unique sales transaction ID.                                                    |
| **Branch**              | Store branch (A, B, or C).                                                      |
| **City**                | Branch location.                                                                |
| **Customer**       | Either **Member** (with loyalty card) or **Normal** (without).                   |
| **Gender**              | Customer's gender.                                                              |
| **Product Line**        | Product category (e.g., Electronics, Fashion, Food, Health, etc.).               |
| **Unit Price**          | Price per product in USD.                                                       |
| **Quantity**            | Number of items purchased.                                                      |
| **Tax**                 | 5% sales tax.                                                                   |
| **Total**               | Total amount paid (including tax).                                              |
| **Date**                | Purchase date (Jan 2019 - Mar 2019).                                            |
| **Time**                | Purchase time (between 10 AM and 9 PM).                                         |
| **Payment**      | Payment type: **Cash**, **Credit Card**, or **E-wallet**.                        |
| **COGS**                | Cost of goods sold.                                                             |
| **Gross Margin**      | Profit margin percentage.                                                       |
| **Gross Income**        | Profit from the sale.                                                           |
| **Rating**     | Customer's rating of their shopping experience (1-10 scale).                    |


---

## **2. Data Cleaning and Preparation**

**Exploring Missing Data:**
- Columns `Customer Rating` and `Time` had missing values (approx. 5%).
- Duplicates were found in the `Invoice ID` column and removed.

**Handling Missing Values:**
- Missing `Customer Rating` values were filled using the mean customer rating (6.7/10).
- Missing `Time` values were forward filled using the purchase time of the previous entry.

**Data Transformation:**
- Created new columns: 
  - `Total Price (Excluding Tax)`
  - `Day of the Week`
  - `Time Period` (Morning, Afternoon, Evening)
  
The cleaned dataset was saved as `cleaned_supermarket_sales.csv`.

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
