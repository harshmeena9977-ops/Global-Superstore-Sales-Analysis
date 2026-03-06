# Technical Documentation

## Data Processing Pipeline

### 1. Data Cleaning & Validation
```sql
-- Key transformations performed:
-- 1. Removed duplicate orders based on Order ID
-- 2. Handled missing values in critical fields
-- 3. Standardized date formats for time-series analysis
-- 4. Created calculated fields for profit margins

SELECT 
    Order_ID,
    Order_Date,
    Ship_Date,
    Customer_ID,
    Product_ID,
    Sales,
    Quantity,
    Discount,
    Profit,
    -- Calculated profit margin
    CASE 
        WHEN Sales > 0 THEN (Profit / Sales) * 100
        ELSE 0 
    END as Profit_Margin_Percent,
    -- Discount impact analysis
    CASE 
        WHEN Discount > 0.25 THEN 'High Discount Risk'
        WHEN Discount > 0.15 THEN 'Medium Discount'
        ELSE 'Low Discount'
    END as Discount_Risk_Level
FROM Global_Superstore_Raw
WHERE Sales > 0 AND Profit IS NOT NULL;
```

### 2. Business Logic Calculations
```sql
-- Category performance analysis
WITH Category_Analytics AS (
    SELECT 
        Category,
        Sub_Category,
        SUM(Sales) as Total_Sales,
        SUM(Profit) as Total_Profit,
        AVG(Discount) as Avg_Discount,
        COUNT(DISTINCT Customer_ID) as Unique_Customers,
        SUM(Quantity) as Total_Quantity
    FROM Global_Superstore_Clean
    GROUP BY Category, Sub_Category
)
SELECT 
    *,
    Profit_Margin = (Total_Profit / Total_Sales) * 100,
    Customer_Value = Total_Sales / Unique_Customers
FROM Category_Analytics
ORDER BY Total_Profit DESC;
```

## Power BI Dashboard Architecture

### Data Model Design
- **Fact Table:** Sales transactions (central fact table)
- **Dimension Tables:** Products, Customers, Geography, Time
- **Relationships:** Star schema with proper cardinality

### Key DAX Measures
```dax
// Total Sales
Total Sales = SUM(Sales[Sales])

// Total Profit
Total Profit = SUM(Sales[Profit])

// Profit Margin
Profit Margin % = 
DIVIDE(
    [Total Profit],
    [Total Sales]
) * 100

// Year-over-Year Growth
YoY Sales Growth = 
VAR CurrentYear = SELECTEDVALUE('Date'[Year])
VAR PreviousYear = CurrentYear - 1
VAR CurrentSales = CALCULATE([Total Sales], 'Date'[Year] = CurrentYear)
VAR PreviousSales = CALCULATE([Total Sales], 'Date'[Year] = PreviousYear)
RETURN 
DIVIDE(
    CurrentSales - PreviousSales,
    PreviousSales
)

// Discount Impact Analysis
High Discount Impact = 
CALCULATE(
    [Total Profit],
    Sales[Discount] > 0.25
)
```

### Visual Components
1. **KPI Cards:** Total Sales, Profit, Margin, Growth
2. **Geographic Maps:** Regional performance with filled maps
3. **Trend Charts:** Year-over-year performance tracking
4. **Bar Charts:** Category and sub-category comparisons
5. **Scatter Plots:** Discount vs. profit analysis

## Performance Optimization

### Data Model Optimization
- **Relationship Cardinality:** Proper one-to-many relationships
- **Column Types:** Optimized data types for storage efficiency
- **Calculated Columns:** Pre-computed complex calculations
- **Measures:** Dynamic calculations for user interactions

### Query Performance
- **Indexing Strategy:** Created indexes on frequently filtered columns
- **Query Folding:** Optimized SQL queries for Power BI integration
- **Memory Management:** Efficient data loading patterns

## Quality Assurance

### Data Validation Rules
1. **Referential Integrity:** All foreign keys validated
2. **Business Logic:** Profit calculations verified
3. **Date Consistency:** Ship date >= Order date
4. **Numeric Validation:** No negative quantities or prices

### Testing Scenarios
```sql
-- Test 1: Profit margin calculations
SELECT 
    Category,
    AVG(Profit / Sales) * 100 as Avg_Margin,
    MIN(Profit / Sales) * 100 as Min_Margin,
    MAX(Profit / Sales) * 100 as Max_Margin
FROM Global_Superstore_Clean
WHERE Sales > 0
GROUP BY Category;

-- Test 2: Discount impact validation
SELECT 
    CASE 
        WHEN Discount > 0.25 THEN 'High Discount'
        WHEN Discount > 0.15 THEN 'Medium Discount'
        ELSE 'Low Discount'
    END as Discount_Category,
    AVG(Profit) as Avg_Profit,
    COUNT(*) as Transaction_Count
FROM Global_Superstore_Clean
GROUP BY 
    CASE 
        WHEN Discount > 0.25 THEN 'High Discount'
        WHEN Discount > 0.15 THEN 'Medium Discount'
        ELSE 'Low Discount'
    END;
```

## Deployment & Maintenance

### Refresh Strategy
- **Data Source:** CSV file updates
- **Refresh Frequency:** Manual refresh for demo purposes
- **Automation:** Power BI Gateway for scheduled updates

### Monitoring
- **Performance Metrics:** Dashboard load times
- **Data Quality:** Automated validation checks
- **User Analytics:** Feature usage tracking

## Troubleshooting Guide

### Common Issues
1. **Slow Dashboard Loading**
   - Check data model relationships
   - Optimize DAX measures
   - Reduce visual complexity

2. **Incorrect Calculations**
   - Verify measure definitions
   - Check filter context
   - Validate data types

3. **Data Refresh Failures**
   - Check data source connectivity
   - Validate file paths
   - Review permissions

### Performance Tips
- Use appropriate visual types for data volume
- Limit number of visuals per page
- Optimize color schemes for clarity
- Implement proper drill-through actions
