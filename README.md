# THE-LOOK-ECOMMERCE-SALES
### Project Overview
 For an eCommerce platform like "The Look," orders analysis helps assess key performance indicators related to sales, customer preferences, and overall revenue.The purpose of this analysis is to analyze the sales performance for the year 2023 in order to access its overall growth, and to understand its traffic and visitor behaviors, in order to inform future planning and optimize profitability for the upcoming fiscal year.

 ### About Dataset.
TheLook is a fictitious eCommerce clothing site developed by the Looker team. The dataset is hosted on Google biq query and contains information about customers, products, orders, logistics, web events and digital marketing campaigns. The dataset currently contains sales transaction information from August 2019 to October 2024, but I will be working with the 2023 data. The contents of this dataset are provided to industry practitioners for the purpose of product discovery, testing, and evaluation. At the time of this analysis, the data set contains sales trasaction from August 2019 to October 2014. But we will be limiting our analysis to 2023. You can access the entire dataset [here](https://cloud.google.com/bigquery/?hl=en)

### Tools
Google big query 

### Data cleaning/preparation 
Since the data was almost already in the right format, The next most important task was to Identify  the primary keys and checking for duplicates and null values when exploring the dataset and also to look for relevant fields that are relevant for the analysis and tables relevant to the analysis.

### Exploratory Data Analysis
EDA involves eploring the dataset to answer questions related to:
- How much did we sell monthly? To analyze monthly order and sales trends in order to identify Seasonality and peak Sales periods.
- Which product categories and brand brought in the most and least revenue and how does this relate to orders?
- Which of the store department brought in the most revenue?
- Where is our customers ordering From?

;;; 
  sql
SELECT FORMAT_DATE('%B', DATE(oi.created_at)) AS month,
COUNT(oi.order_id) AS order_count, 
ROUND(SUM(sale_price * num_of_item),1) AS Revenue,
COUNT(DISTINCT oi.user_id) AS customers
FROM `bigquery-public-data.thelook_ecommerce.order_items` 
AS oi
INNER JOIN `bigquery-public-data.thelook_ecommerce.orders` 
AS o
ON oi.order_id = o.order_id
WHERE oi.status NOT IN ('Cancelled', 'Returned') AND EXTRACT(year FROM oi.created_at) = 2023
GROUP BY month
ORDER BY order_count DESC;
;;;
