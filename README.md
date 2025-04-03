# SQL-Sales-Analysis <br/>

## 3. Query Breakdown <br/> 
### Query 1: Yearly Sales Analysis <br/> <br/> 
```sql
SELECT year_id, ROUND(SUM(sales), 2) AS total_sales 
FROM sales_data 
GROUP BY year_id 
ORDER BY year_id; 
```
**Purpose**: The goal of this query is to assess yearly sales performance and determine whether the company experienced growth, decline, or stagnation over time. This gives me a base understanding and view before diving into the more detailed and specific trends. <br/> <br/> 
**Findings**: <br/> 
* 2003: Sales fluctuated throughout the earlier months but showed a strong spike in November-December, likely due to a holiday demand. <br/>
* 2004: Sales were more consistent throughout the year, with a steady increase in the first 10 months compared to 2003. Since the growth was consistent, this suggests either business expansion or improved sales strategies, as it wasn’t just an arbitrary period of a few months. <br/>
* 2005: Showed strong early-year sales, in contrast to the slower starts to the year from 2003 and 2004. This could indicate a new sales strategy the company may have implemented, aimed at maintaining momentum year-round after experiencing slower starts to the year in 2003 and 2004 <br/> <br/>

### Query 2: Monthly Sales Trends  <br/>  <br/> 
```sql
SELECT year_id, month_id, SUM(sales) AS total_sales 
FROM sales_data
GROUP BY year_id, month_id 
ORDER BY year_id, month_id;
```
**Purpose**: The goal of this query is to analyze sales data on a monthly basis to identify seasonal patterns and trends, following up on the yearly analysis. By examining monthly sales, I can pinpoint specific months that tend to perform better. This analysis helps to uncover seasonality and specific periods where the company experiences peak demand in its product. <br/> <br/> 
**Findings**: <br/> 
* Seasonality and Summer Peaks (May-August): Across all three years (2003, 2004 and 2005), there was a clear pattern with significant spikes in sales during these months. Since this is a northern hemisphere dataset, the data suggests a key demand for this product during the summer months. Possible factors are due to warmer weather, vacations, or specific seasonal sales campaigns. <br/>
* End-Of-Year Surge (November-December): Both 2003 and 2004 showed a strong spike in sales, which indicates a successful end of year push or holiday-related demand or end of year promotions. Due to these months consistently outperforming the others each year, it indicates the effectiveness of year-end sales or a seasonal sales push. <br/>
* Early-Year Slowdown (January-February): With the exception of 2005, January and February were consistently lower in sales during the previous years. This could indicate a stronger push to the beginning of the year in 2005, after 2 prior years of slower starts in respect to sales. <br/> <br/>

### Query 3: Product Line Performance <br/> <br/> 
```sql
SELECT product_line, ROUND(SUM(sales), 2) AS total_sales
FROM sales_data
GROUP BY product_line
ORDER BY total_sales DESC;  
```
**Purpose**: The goal of this query is to analyze total sales by product line to determine which vehicle categories contribute the most to overall revenue. By understanding which product lines are most and least profitable, the company can make data-driven decisions about marketing strategies and potential areas for growth. This helps identify which products drive significant revenue and whether any underperforming product lines need further investigation. <br/> <br/> 
**Findings**: <br/> 
* Classic Cars Dominate Sales ($3.92M): Classic cars are the highest-performing product line. This suggests a strong demand for this product in the market, possibly due to collectors or enthusiasts who are willing to pay premium prices. The company may want to further invest in this segment by expanding inventory or introducing new models as part of their sales. <br/>
* Vintage Cars Perform Well ($1.90M): Vintage cars had the second–highest sales, showing that the demand for collectable and nostalgic vehicles is a consistent pattern throughout this sales data. This could indicate an opportunity to capitalize further on older limited-edition models. <br/>
* Motorcycles, Trucks, and Buses are Mid-Tier Performers: While these categories of products did make an impact and contribute significantly to overall revenue, they underperform compared to Classic and Vintage Cars. <br/>
* Planes and Ships Have Lower Sales ($975K, $714K): These two products generated significantly less revenue than the top-performing categories. This could be due to a more niche market, higher costs, and/or lower demand. <br/>
* Trains are the least profitable ($226K): Trains had the lowest sales, making them the weakest-performing product line. The company may need to reassess its approach to selling trains, considering factors such as pricing, demand, or marketing strategy. <br/> <br/>

**Market Considerations**: <br/> <br/> 

* Classic and Vintage Cars Likely Benefit from Individual Customers: One possible reason for the dominance of Classic Cars and Vintage Cars is that they are more accessible to individual buyers. Unlike planes, ships, and trains - Which are likely purchased by corporations or businesses. Cars appeal to a broader consumer market, including collectors, enthusiasts, and everyday drivers. The affordability, practicality, and emotional connection to classic and vintage cars could be driving higher sales volumes. <br/>
* Trains, Ships and Planes May Cater to a Niche Market: The lower sales figures for Trains ($226K), Ships ($714K), and Planes ($975k) could be attributed to their specialized nature. These products are more likely purchased by businesses, government agencies, or large transport firms, which may have longer purchasing cycles, higher budget constraints or more selective procurement process compared to individual buyers. <br/> <br/>        
  
### Query 4: Customer Purchase Frequency Analysis  <br/>  <br/> 

#### Query 4.1 Finding the Top Customers Based on Revenue
```sql
SELECT customer_name,
       COUNT(ordernumber) AS total_orders,
       ROUND(SUM(sales), 2) AS total_sales 
FROM sales_data 
GROUP BY customer_name 
ORDER BY total_sales DESC 
LIMIT 10;
```
**Purpose**: The purpose of this query is to identify the top 10 customers based on total revenue generated. By analyzing which customers contribute the most to overall sales, the company can prioritize customer relationships, develop targeted marketing strategies, and explore potential opportunities for repeat business. This can highlight key accounts to maintain strong relationships with. <br/> <br/> 
**Findings**: <br/> 
#### 1. Euro Shopping Channel is the highest-revenue customer ($912K, 259 orders) <br/> 
* This customer significantly outperforms all others, contributing nearly $1 million in sales. <br/>
* With 259 total orders, their frequent purchases make them a high-value client, likely operating as a bulk buyer or distributor. <br/>
#### 2. Mini Gifts Distributors Ltd. ranks second ($654K, 180 orders) <br/> 
* A strong contributor to revenue, but still significantly behind Euro Shopping Channel. <br/>
* The high number of orders suggests they may also be a bulk retailer or corporate client. <br/>
#### 3. Significant revenue gap after the top two customers <br/> 
* The third-highest customer (Australian Collectors, Co.) generated $200K, which is less than one-third of the second-place customer. Suggesting the top two customers contribute a disproportionately large share of total sales <br/>
#### 4. Orders vs. Revenue: Higher sales don’t always mean more orders <br/> 
* Some customers, like "La Rochelle Gifts" and "Muscle Machine Inc.," placed fewer orders than others but still had comparable total sales. <br/>
* This may indicate that certain customers place larger individual orders with higher-value products. <br/>
#### 5. Diversity in customer base <br/> 
* The top 10 customers appear to include a mix of gift distributors, specialty retailers, and collectors.
* Some, like "Dragon Souvenirs, Ltd." and "Land of Toys Inc.," suggest niche markets, while others like "AV Stores, Co." and "The Sharp Gifts Warehouse" may have broader sales models. <br/>
**Business Implications & Next Steps**: <br/>
  * Customer Retention: Since the top two customers contribute a substantial portion of revenue, the company should focus on maintaining strong relationships with them. This may include personalized offers, volume discounts, or loyalty incentives.
  * Growth Opportunities: Given the revenue gap, the company might want to explore why the third-ranked customer contributes significantly less than the second, and whether or not there untapped opportunities to increase sales with them. <br/> <br/>
  #### Query 4.2 Adding an Average Order Value Column
```sql
  SELECT customer_name, 
       COUNT(ordernumber) AS total_orders, 
       ROUND(SUM(sales), 2) AS total_sales,
       ROUND(AVG(sales), 2) AS avg_order_value
FROM sales_data
GROUP BY customer_name
ORDER BY total_sales DESC
LIMIT 10;
```
**Purpose**: The purpose of this query is to calculate the average order value (AOV) for the top customers based on their total sales. This metric helps to understand how much, on average, customers are spending per order, providing insights into purchasing behavior. By calculating the AOV for each top customer, the company can identify which customers are making larger, more valuable purchases. The analysis helps to assess the profitability of customers and informs decisions on targeted sales strategies and potential pricing adjustments. <br/> <br/> 
**Findings**: <br/> 
#### High-Value Customers: 
* The customer with the highest average order value is Muscle Machine Inc., with an AOV of $4119.52. This suggests that, although they place fewer orders, they are purchasing higher-value items. The company could explore strategies to target customers like this with premium product offerings or incentives for continued high-value purchases.
* The second-highest AOV is Dragon Souveniers, Ltd. at $4023.02, indicating a strong purchasing tendency toward high-value products.
