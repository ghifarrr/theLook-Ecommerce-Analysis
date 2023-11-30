# theLook Ecommerce Analysis
TheLook is a fictitious eCommerce clothing site developed by the Google Looker team. The dataset contains information about customers, products, orders, logistics, web events and digital marketing campaigns. The contents of this dataset are synthetic, and are provided to industry practitioners for the purpose of product discovery, testing, and evaluation.
At the time of this analysis, the e-commerce store recorded sales transaction data from January 2022 to December 2022. 

This dataset can be accessed through google bigquery public data, where the query below is run with SQL Bigquery Studio. The analysis used on theLook Ecommerce dataset is the cohort analysis method, which is a technique used to analyze and understand the behavior of a group of individuals over time. In cohort analysis, individuals are grouped based on their characteristics, such as when they signed up for a service or purchased a product. 
And what is done in this project is Cohort retention rate analysis which is a metric that measures the percentage of customers who continue to repurchase with a company over time. To calculate the cohort retention rate, a business first defines a cohort of customers based on a common characteristic or behavior, such as the month in which they made their first purchase.

## Scope of Problem
How many users coming back to reorder for the following months in 2022?

Solution:

![alt text](https://github.com/ghifarrr/theLook-Ecommerce-Analysis/blob/main/Pics/pic1.png?raw=true)
![alt text](https://github.com/ghifarrr/theLook-Ecommerce-Analysis/blob/main/Pics/pic2.png?raw=true)

This query above is used to analyze the user retention rate for theLook E-Commerce. 
The query is composed of several Common Table Expressions (CTEs), which are similar to subqueries but allow you to name and reuse the results.

- cohort_customer: This CTE selects all distinct users and their first purchase date from the orders table. The first purchase date is determined by taking the minimum of all dates in each user's order history.
- user_activities: This CTE joins the orders table with the cohort_customer table. It then calculates the difference in months between the order's date and the user's first purchase date.
- cohort_size: This CTE groups the cohort_customer table by the first purchase date and counts the number of users in each cohort.
- retention_table: This CTE groups the user_activities table by the first purchase date and month number, and counts the number of users in each group.

Finally, the query joins the retention_table with the cohort_size table to calculate the retention rate. It returns the first purchase date, cohort size, month number, total number of users, and the percentage of users who made a purchase within that month.
The output of this query is used to analyze user retention patterns and identify areas for improvement. Where the output results of this query are moved to Google Sheets, the results are processed with a pivot table to produce a table in the form of a period table, which contains the number of users along with the user retention rate every month in 2022.
 
![alt text](https://github.com/ghifarrr/theLook-Ecommerce-Analysis/blob/main/Pics/pic3.png?raw=true)

From this table above we can analyze and conclude, there is a massive drop in retention rates entering the first month since they first placed an order. It can be seen in the cohort table above that the average user retention rate drops drastically from 100% to ±3% in the next month, it can be concluded that users are returning less and less since they first placed an order. However, each cohort's retention rate has increased and decreased steadily at 2.94% - 3.69% every month from the beginning of the user's order. We can see that the August to November cohort has a higher retention rate than the previous months, where the retention rate value is at 2.77% - 4.83% in the month after the first user places an order. Then we can find out that the September cohort has the largest retention rate after its first order in the first month after its first order at 4.83%, and the March cohort has the largest decrease in user retention rate with 2.48% in its third month. Although this  retention value is a very small value that requires improvement and evaluation of a more effective business strategy.

## Hypothesis
What could possibly the main reason we have so low retention rate?
After exploring data I used Univariate analysis, which analyzes the columns separately and looks at the distribution of the data. Then I would check the status of order_items data and check the total number of orders that exist in each status, at the time is the reason why a lot of cohort size have drop retention on the first month after their order.

![alt text](https://github.com/ghifarrr/theLook-Ecommerce-Analysis/blob/main/Pics/pic4.png?raw=true)

The hypothesis that I get is by analyzing the data obtained from various tables on thelook ecomerce dataset, where a conclusion is obtained from a large hole that can be seen in the item order’s status column. That there are many customer item order statuses that are canceled and returned, with a canceled percentage of 15.09% and a returned percentage of 10.04%, that means 25.14% of the items seems failed to be sold, this percentage value is very huge seeing from the orders completed in 2022 only 24.85% of which the rest are still in process and shipping. 
This indicates that the seller canceled or sent items that were not supposed to be, which can be a red flag for potential customers to return to the store or even for the reputation of thelook ecommerce it self. 

![alt text](https://github.com/ghifarrr/theLook-Ecommerce-Analysis/blob/main/Pics/pic%205.png?raw=true)

## Recommendation
For seller: 
- It is important for the seller to monitor its cancellation rate and better understand how to reduce it if it exceeds the required threshold. 
- A high cancellation rate can be caused by many factors such as poor inventory management, product listing errors, or communication issues with customers,etc. By improving these areas, sellers can reduce the cancellation and return rates thus providing a better experience for their customers.

For thelook ecommerce:
- Thelook has the right to make regulations that benefit both buyers and sellers. So it is necessary to make rules that set limits on stores canceling orders unilaterally and conduct further analysis if a store often experiences returns from buyers.
