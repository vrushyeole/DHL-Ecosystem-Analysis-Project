# DHL Logistics Advanced SQL & Power BI Project

## Project Overview
This project addresses key business challenges in a DHL-like logistics environment using advanced SQL techniques. By leveraging a star schema data warehouse hosted on SQL Server, we extract actionable insights from logistics operations. These insights are then integrated into interactive Power BI dashboards for real-time and historical analysis. The project demonstrates advanced analytics in areas such as delivery performance, fuel efficiency, warehouse operations, customer behavior, and more.

## Objectives
- **Optimize Delivery Performance:** Identify and reduce delivery delays to improve customer satisfaction.
- **Enhance Cost Efficiency:** Analyze fuel consumption, operational costs, and route efficiency.
- **Improve Warehouse Operations:** Evaluate processing times to pinpoint inefficiencies.
- **Drive Customer Insights:** Identify high-value customers and assess order frequency.
- **Strengthen Regional Analysis:** Compare performance metrics across regions to inform resource allocation.
- **Implement Advanced Security:** Enforce role-based access to sensitive operational data.

## Business Problems & SQL Solutions

The project includes a comprehensive set of SQL queries to tackle complex logistics problems. Below is a summary of key business problems and the corresponding SQL tasks implemented:

1. **Monthly On-Time Delivery Performance Analysis**  
   - **Problem:** Delivery delays reduce customer satisfaction and increase costs.  
   - **Solution:** Aggregate monthly trip data to calculate total trips, on-time trips, on-time percentages, and average delivery delays using basic grouping, CASE expressions, and DATEDIFF.

2. **Fuel Cost per Mile by Vehicle**  
   - **Problem:** High fuel costs impact profitability.  
   - **Solution:** Compute fuel cost per mile by vehicle using aggregations with safeguards against division by zero.

3. **Average Warehouse Processing Time Analysis**  
   - **Problem:** Inefficient warehouse processes lead to delays and increased costs.  
   - **Solution:** Calculate the average processing time for trips by warehouse using JOINs and AVG aggregation.

4. **Delay Distribution Analysis**  
   - **Problem:** Understanding delay distributions is essential for targeted improvements.  
   - **Solution:** Categorize trips into delay buckets (e.g., 0-5, 5-10, 10-15, 15+ minutes) using CASE expressions and aggregate frequency counts.

5. **Ranking Warehouses by On-Time Delivery**  
   - **Problem:** Evaluating warehouse performance helps drive operational improvements.  
   - **Solution:** Rank warehouses based on on-time delivery percentages using aggregation and the RANK() window function.

6. **Identify Customers with Mismatched Pickup Locations**  
   - **Problem:** Shipments picked up from locations different from the customer’s registered address may indicate special handling or decentralized operations.  
   - **Solution:** Use correlated subqueries (EXISTS) to list customers with mismatched pickup locations.

7. **Customers with Above-Average Order Frequency**  
   - **Problem:** Identifying high-value customers based on order frequency enables targeted marketing and loyalty programs.  
   - **Solution:** Retrieve customers whose trip counts exceed the overall average using nested subqueries for aggregation.

8. **Impact Analysis of Traffic Conditions on Delivery Performance**  
   - **Problem:** Varying traffic conditions can significantly affect delivery times and fuel efficiency.  
   - **Solution:** Aggregate data by traffic condition to quantify its impact on average delivery delays and fuel cost per mile.

9. **Cost Efficiency Analysis Across Regions**  
   - **Problem:** Operational costs vary across regions due to differing logistical challenges.  
   - **Solution:** Calculate the operational cost per mile by region by joining trip and customer data.

10. **Cumulative Delay Calculation Using Window Functions**  
    - **Problem:** Accumulated delays over time may indicate systemic issues.  
    - **Solution:** Compute a running total of delivery delays per vehicle using window functions with SUM() OVER.

11. **Regional Demand Growth Analysis**  
    - **Problem:** Different regions may experience varying growth in shipment demand, affecting capacity planning.  
    - **Solution:** Calculate month-over-month growth in trip volumes for each region using window functions (LAG) within a CTE.

12. **Identify Pickup Locations with High Trip Volume and Low On-Time Performance**  
    - **Problem:** Some pickup locations have high volumes but poor performance.  
    - **Solution:** Compare on-time performance per pickup location against the overall average using subqueries and filter for the top 5 problematic locations.

13. **Customer Order Frequency Analysis**  
    - **Problem:** Understanding customer ordering patterns helps identify high-value customers.  
    - **Solution:** Use nested subqueries to retrieve customers whose order frequency exceeds the overall average.

14. **Predictive Maintenance Indicator with Recursive CTE**  
    - **Problem:** Rising delays for a vehicle may signal maintenance issues.  
    - **Solution:** Compare monthly average delays using recursive CTEs and LAG() to flag vehicles with increasing delays.

15. **Complex Multi-Dimensional Join for Consolidated View**  
    - **Problem:** A unified view is needed for comprehensive logistics tracking.  
    - **Solution:** Create a view that joins the Trips fact table with all related dimension tables.

16. **Dynamic SQL for Ad-Hoc Reporting**  
    - **Problem:** Stakeholders require flexible, parameter-driven reports.  
    - **Solution:** Develop a stored procedure that constructs and executes dynamic SQL based on user inputs.

17. **Advanced Statistical Analysis for Risk Management**  
    - **Problem:** High variability in delivery delays can indicate operational risks.  
    - **Solution:** Use STDEV and PERCENTILE_CONT to calculate statistical metrics for delays by month.

18. **Real-Time Anomaly Detection Using SQL Triggers**  
    - **Problem:** Prompt detection of anomalies is crucial for operational responsiveness.  
    - **Solution:** Create a trigger that logs trips with delays exceeding 120% of the estimated travel time into an anomaly table.

19. **Nested CTEs for Multi-Level Aggregation**  
    - **Problem:** Detailed trend analysis requires data aggregated at multiple levels (daily, monthly).  
    - **Solution:** Use nested CTEs to first summarize daily data, then roll it up into monthly aggregates.

20. **Implementing Role-Based Security (RLS) for Sensitive Data**  
    - **Problem:** Sensitive operational data must be accessible only to authorized users.  
    - **Solution:** Configure Row-Level Security (RLS) using security predicate functions to restrict data access based on user roles.

## Power BI Integration
- **Data Sources:** SQL views, aggregated summary tables, and stored procedures.
- **Visualization:** Power BI dashboards display interactive visuals such as line charts, bar charts, scatter plots, and matrices based on the SQL query outputs.
- **Real-Time Reporting:** DirectQuery or scheduled refresh ensures up-to-date dashboards reflecting the latest operational data.

## Technologies Used
- **SQL Server:** Hosts the star schema data warehouse.
- **Advanced SQL Techniques:** Window functions, recursive CTEs, dynamic SQL, subqueries, and indexing.
- **Power BI:** Used for creating interactive dashboards and real-time analytics.
- **Optional ETL Tools:** Python for automation and additional data transformations.

## Repository Structure
