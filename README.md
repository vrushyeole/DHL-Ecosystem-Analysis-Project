# DHL Ecosystem Advanced SQL & Power BI Analysis Project

This repository demonstrates a comprehensive, real-time transportation and logistics performance optimization system modeled after a DHL-like environment. The solution leverages advanced SQL techniques on a star schema data warehouse (hosted in SQL Server) along with interactive Power BI dashboards to provide actionable insights into complex logistics business problems.

---

## Table of Contents

- [Overview & Objectives](#overview--objectives)
- [Business Problems & Goals](#business-problems--goals)
- [Data Modeling & Schema Design](#data-modeling--schema-design)
- [ETL Process](#etl-process)
- [Advanced SQL Analysis Tasks](#advanced-sql-analysis-tasks)
  - [Intermediate-Level Tasks](#intermediate-level-tasks)
  - [Advanced-Level Tasks](#advanced-level-tasks)
- [Power BI Dashboard & Analytics](#power-bi-dashboard--analytics)
- [Implementation Roadmap](#implementation-roadmap)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## Overview & Objectives

**Overview:**  
This project builds a real-time transportation and logistics performance optimization system. Data from multiple operational sources (trips, vehicles, warehouses, locations, external factors, and customer details) is consolidated into a centralized star schema data warehouse hosted on SQL Server. Advanced SQL queries extract deep insights from the data, and these insights are visualized in interactive Power BI dashboards to support both operational and strategic decision-making.

**Objectives:**

- **Data Integration:** Consolidate disparate data sources into a unified, scalable data warehouse.
- **Real-Time & Historical Analysis:** Support live monitoring (via DirectQuery in Power BI) as well as historical trend analysis.
- **Operational Efficiency:** Optimize delivery performance, route planning, fuel consumption, and warehouse processing.
- **Informed Decision-Making:** Provide interactive dashboards and advanced SQL analytics to drive cost reduction and improve service levels.
- **Scalability:** Design a modular system that can evolve with additional dimensions and KPIs over time.

---

## Business Problems & Goals

**Business Problems Addressed (Taskwise):**

1. **Delivery Delays & Inefficiencies:**  
   Identify bottlenecks causing frequent delivery delays.
2. **High Operational Costs:**  
   Monitor fuel consumption and maintenance to reduce expenses.
3. **Fragmented Data:**  
   Unify data across TMS, WMS, CRM, etc., for a complete operational view.
4. **Lack of Real-Time Visibility:**  
   Provide live insights for quick responses to disruptions.
5. **Inadequate Historical Insights:**  
   Analyze long-term trends for strategic planning.
6. **Underutilized Vehicles:**  
   Detect poor load management leading to wasted capacity.
7. **Inefficient Warehouse Operations:**  
   Measure processing times to identify bottlenecks in warehouse performance.
8. **Predictive Maintenance Challenges:**  
   Forecast potential vehicle breakdowns through trend analysis.
9. **Carrier Performance Variability:**  
   Rank and analyze carrier/vehicle performance for reliability.
10. **Risk Management & Compliance:**  
    Identify anomalies and operational risks to support compliance efforts.

**Business Goals:**

- **Improve On-Time Delivery:** Reduce delays through optimized routing and scheduling.
- **Reduce Costs:** Optimize fuel consumption and operational processes.
- **Unify Data Silos:** Integrate multiple data sources into a single, unified warehouse.
- **Enhance Real-Time Monitoring:** Enable proactive decision-making with live dashboards and alerts.
- **Drive Strategic Insights:** Leverage historical data for forecasting and capacity planning.

---

## Data Modeling & Schema Design

**Star Schema Structure (Excluding Date Table):**

- **Fact Table: Trips**  
  - Contains transactional data for each trip (timestamps, distances, travel times, fuel consumption, costs, etc.) and a [Date] column used for filtering.

- **Dimension Tables:**
  - **Vehicle:** Stores details such as VehicleID, VehicleType, and VehicleCapacity.
  - **Warehouse:** Contains full warehouse details including WarehouseID, WarehouseName, Address, City, State, Country, and ZIP.
  - **Location:** Maintains comprehensive addresses for pickup and dropoff points with LocationID, Address, City, State, Country, ZIP, Latitude, and Longitude.
  - **ExternalFactors:** Captures contextual conditions such as TrafficCondition and WeatherCondition.
  - **Customer:** Holds customer information like CustomerID, CustomerName, Address, City, State, Country, ZIP, CustomerType, and Region.

*Note: The Date dimension will be generated in Power BI using built-in functions (e.g., CALENDAR) and linked via the [Date] column in the Trips table.*

---

## ETL Process

1. **Extraction:**  
   - Synthetic CSV files are used for Vehicle, Warehouse, Location, ExternalFactors, Customer, and Trips.
   
2. **Transformation:**  
   - **Data Cleansing:** Standardize addresses, convert timestamp strings to SQL Server DATETIME, and validate numerical fields.
   - **Business Rules:** Derive calculated fields (e.g., delivery delay, fuel cost per mile).
   - **Staging (Optional):** Load raw data into staging tables before applying transformations.

3. **Loading:**  
   - **Dimension Tables:** Load first using BULK INSERT or SSIS.
   - **Fact Table (Trips):** Load after dimensions, ensuring foreign key integrity.
   - **Incremental/Real-Time Updates:** Configure periodic updates to simulate near-real-time analytics.

---

## Advanced SQL Analysis Tasks

### Intermediate-Level Tasks

1. **Monthly On-Time Delivery Performance Analysis:**  
   - **Challenge:** Handle inconsistent date formats.
   - **Solution:** Group by year and month using aggregation and CASE statements.

2. **Fuel Cost per Mile by Vehicle:**  
   - **Challenge:** Avoid division by zero.
   - **Solution:** Aggregate fuel cost and route distance; compute cost per mile safely.

3. **Average Warehouse Processing Time Analysis:**  
   - **Challenge:** Filter out outliers.
   - **Solution:** Aggregate processing times and count trips by warehouse.

4. **Daily Trip Volume Reporting:**  
   - **Challenge:** Ensure complete date coverage.
   - **Solution:** Group trips by the [Date] column.

5. **Customer Order Frequency Analysis:**  
   - **Challenge:** Manage incomplete customer records.
   - **Solution:** Join Trips and Customer, then group by CustomerID.

6. **Basic End-to-End Tracking View:**  
   - **Challenge:** Ensure correct multi-table joins.
   - **Solution:** Create a view that consolidates data from Trips and all dimension tables.

7. **Delay Distribution Analysis:**  
   - **Challenge:** Define meaningful delay ranges.
   - **Solution:** Use CASE statements to bucket delays and aggregate counts.

8. **Average Travel Time by Distance Range:**  
   - **Challenge:** Define optimal distance brackets.
   - **Solution:** Segment trips by distance ranges and compute average travel times.

9. **Ranking Warehouses by On-Time Delivery:**  
   - **Challenge:** Handle ties in performance metrics.
   - **Solution:** Use RANK() over aggregated on-time percentages.

10. **Total Operational Cost per Month:**  
    - **Challenge:** Manage missing cost data.
    - **Solution:** Group by year and month, then sum operational costs.

### Advanced-Level Tasks

11. **Cumulative Delay Calculation Using Window Functions:**  
    - **Challenge:** Correctly partition data.
    - **Solution:** Use SUM() OVER with partitioning by VehicleID.

12. **Predictive Maintenance Indicator with Recursive CTE:**  
    - **Challenge:** Manage recursion limits.
    - **Solution:** Use a recursive CTE with LAG() to flag increasing delays.

13. **Dynamic SQL for Ad-Hoc Reporting:**  
    - **Challenge:** Ensure security and efficiency.
    - **Solution:** Create a stored procedure using sp_executesql with parameters.

14. **Complex Multi-Dimensional Join for Consolidated View:**  
    - **Challenge:** Balance join complexity and performance.
    - **Solution:** Build a comprehensive view joining Trips with all dimensions.

15. **Advanced Statistical Analysis for Risk Management:**  
    - **Challenge:** Interpret statistical metrics.
    - **Solution:** Use STDEV() and PERCENTILE_CONT() to analyze delay variability.

16. **Time-Series Forecasting with Moving Averages:**  
    - **Challenge:** Select an appropriate window frame.
    - **Solution:** Use moving averages with window functions to forecast trends.

17. **Real-Time Anomaly Detection Using SQL Triggers:**  
    - **Challenge:** Minimize performance overhead.
    - **Solution:** Create an AFTER INSERT trigger to log trips with delays exceeding thresholds.

18. **Nested CTEs for Multi-Level Aggregation:**  
    - **Challenge:** Manage nested CTE complexity.
    - **Solution:** Aggregate daily data into monthly summaries using nested CTEs.

19. **Query Optimization with Execution Plans and Query Hints:**  
    - **Challenge:** Interpret and act on execution plan feedback.
    - **Solution:** Analyze execution plans, add query hints (e.g., OPTION (RECOMPILE)), and refine indexes.

20. **Implementing Role-Based Security (RLS) for Sensitive Data:**  
    - **Challenge:** Configure granular access without impacting performance.
    - **Solution:** Create a security predicate function and apply a security policy to restrict data access.

---

## Power BI Dashboard & Analytics

- **Dashboard Development:**  
  Connect Power BI to your SQL Server using DirectQuery or scheduled refresh.  
  Create interactive dashboards to visualize:
  - Monthly on-time performance, average delays, and operational costs.
  - Fuel consumption and cost efficiency by vehicle.
  - Warehouse processing efficiency and inventory turnover.
  - Vehicle utilization, predictive maintenance indicators, and carrier performance.
  - Real-time fleet tracking and anomaly detection metrics.

- **Date Dimension:**  
  In Power BI, generate a Date table using CALENDAR or CALENDARAUTO functions, then relate it to the [Date] column in the Trips table to enable robust time intelligence.

---

## Implementation Roadmap

**Day 1:**  
- Set up SQL Server environment and create a new database.
- Deploy the star schema by executing T-SQL scripts for Vehicle, Warehouse, Location, ExternalFactors, Customer, and Trips.
- Configure advanced settings like indexing.
- Load synthetic CSV data into the tables using BULK INSERT or an ETL tool.

**Day 2:**  
- **Morning Session:**  
  Implement and test 10 intermediate-level tasks and then 10 advanced-level tasks as detailed above.  
  Document each task’s query, the business problem addressed, and challenges encountered.
- **Afternoon Session:**  
  Create aggregated views, perform data quality checks, and optimize query performance using execution plans.
  Commit all scripts and documentation to Git.

**Day 3:**  
- Develop Power BI dashboards that connect to the SQL Server data warehouse.
- Use DirectQuery for real-time analysis and integrate the Power BI-generated Date dimension.
- Finalize and test dashboard interactivity, drill-downs, and alerts.
- Prepare portfolio documentation and demo videos/screenshots.

---

## Repository Structure

