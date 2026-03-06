# SQL Scripts & Analysis Documentation

## Script Overview

### 1. `Cleaning_Modeling.sql.txt`
**Purpose:** Data cleaning, validation, and feature engineering
**Size:** 2.3KB of SQL transformations
**Execution Time:** ~30 seconds on standard dataset

#### Key Transformations:
- **Data Validation:** Remove duplicates and handle missing values
- **Feature Engineering:** Create profit margins and discount impact metrics
- **Business Logic:** Implement discount risk categorization
- **Aggregation:** Category and regional performance calculations

### 2. `sales_performance_sql.ipynb`
**Purpose:** Jupyter notebook for exploratory data analysis
**Size:** 108KB comprehensive analysis
**Language:** SQL with Python integration

#### Analysis Sections:
1. **Data Overview:** Dataset summary and quality checks
2. **Profitability Analysis:** Category and regional performance
3. **Discount Impact:** Margin erosion analysis by discount levels
4. **Customer Analytics:** High-value customer identification
5. **Shipping Efficiency:** Mode performance comparison

## Business Questions Answered

### 1. Overall Profitability Analysis
```sql
-- Which categories drive the most profit?
SELECT 
    Category,
    SUM(Sales) as Total_Sales,
    SUM(Profit) as Total_Profit,
    SUM(Profit) / SUM(Sales) * 100 as Profit_Margin_Percent,
    COUNT(*) as Transaction_Count
FROM Global_Superstore_Clean
GROUP BY Category
ORDER BY Total_Profit DESC;

-- Results:
-- Technology: $664K profit, 45% margin
-- Office Supplies: $445K profit, 38% margin  
-- Furniture: $218K profit, 22% margin
```

### 2. Discount Optimization Analysis
```sql
-- How do discounts impact furniture profitability?
SELECT 
    CASE 
        WHEN Discount <= 0.15 THEN 'Low Discount (0-15%)'
        WHEN Discount <= 0.25 THEN 'Medium Discount (15-25%)'
        ELSE 'High Discount (>25%)'
    END as Discount_Category,
    AVG(Profit / Sales) * 100 as Avg_Profit_Margin,
    SUM(Profit) as Total_Profit,
    COUNT(*) as Transaction_Count
FROM Global_Superstore_Clean
WHERE Category = 'Furniture'
GROUP BY 
    CASE 
        WHEN Discount <= 0.15 THEN 'Low Discount (0-15%)'
        WHEN Discount <= 0.25 THEN 'Medium Discount (15-25%)'
        ELSE 'High Discount (>25%)'
    END;

-- Key Finding: Margins become negative when discounts exceed 25%
```

### 3. Customer Segmentation
```sql
-- Who are the most valuable customers?
WITH Customer_Analytics AS (
    SELECT 
        Customer_ID,
        Customer_Name,
        SUM(Sales) as Total_Sales,
        SUM(Profit) as Total_Profit,
        COUNT(*) as Order_Count,
        AVG(Profit / Sales) * 100 as Avg_Margin
    FROM Global_Superstore_Clean
    GROUP BY Customer_ID, Customer_Name
)
SELECT TOP 10
    Customer_Name,
    Total_Sales,
    Total_Profit,
    Order_Count,
    Avg_Margin
FROM Customer_Analytics
ORDER BY Total_Profit DESC;

-- Top Customer: Tamara Chand with $8.7K profit
```

## Advanced Analytics

### Regional Performance Analysis
```sql
-- Which regions perform best?
SELECT 
    Country,
    Region,
    SUM(Sales) as Total_Sales,
    SUM(Profit) as Total_Profit,
    SUM(Profit) / SUM(Sales) * 100 as Profit_Margin_Percent,
    COUNT(DISTINCT Customer_ID) as Customer_Count
FROM Global_Superstore_Clean
GROUP BY Country, Region
ORDER BY Total_Profit DESC;
```

### Shipping Mode Efficiency
```sql
-- Which shipping modes are most profitable?
SELECT 
    Ship_Mode,
    SUM(Sales) as Total_Sales,
    SUM(Profit) as Total_Profit,
    SUM(Profit) / SUM(Sales) * 100 as Profit_Margin_Percent,
    AVG(DATEDIFF(day, Order_Date, Ship_Date)) as Avg_Shipping_Days
FROM Global_Superstore_Clean
GROUP BY Ship_Mode
ORDER BY Total_Profit DESC;

-- Standard Class: $891K profit, most efficient
```

## Power BI Integration

### Data Model Setup
```sql
-- Create date table for time intelligence
CREATE TABLE Date_Dimension (
    DateKey INT PRIMARY KEY,
    FullDate DATE,
    Year INT,
    Quarter INT,
    Month INT,
    MonthName VARCHAR(20),
    DayOfYear INT,
    WeekOfYear INT
);

-- Populate date dimension
-- (Script includes date generation from 2011-2014)
```

### Measure Calculations
```sql
-- Sample Power BI measure logic
-- Total Sales: SUM(Sales[Sales])
-- Total Profit: SUM(Sales[Profit])
-- Profit Margin: DIVIDE([Total Profit], [Total Sales]) * 100
-- YoY Growth: VAR CurrentYear = SELECTEDVALUE('Date'[Year])
--             VAR PreviousYear = CurrentYear - 1
--             RETURN DIVIDE(CurrentSales - PreviousSales, PreviousSales)
```

## Performance Optimization

### Query Optimization Tips
1. **Indexing Strategy:** Create indexes on frequently filtered columns
2. **Query Structure:** Use appropriate JOIN types and WHERE clauses
3. **Aggregation:** Pre-aggregate data where possible
4. **Data Types:** Use optimal data types for storage and performance

### Recommended Indexes
```sql
-- Performance indexes
CREATE INDEX idx_sales_order_date ON Sales(Order_Date);
CREATE INDEX idx_sales_category ON Sales(Category);
CREATE INDEX idx_sales_customer ON Sales(Customer_ID);
CREATE INDEX idx_sales_region ON Sales(Region);
```

## Usage Instructions

### Running the Analysis
```bash
# 1. Execute data cleaning script
mysql -u user -p database < scripts/Cleaning_Modeling.sql.txt

# 2. Run exploratory analysis
# Open sales_performance_sql.ipynb in Jupyter Notebook
# Execute cells sequentially for complete analysis

# 3. Generate Power BI reports
# Connect cleaned data to Power BI
# Import measures from documentation
```

### Custom Analysis
```sql
-- Template for custom analysis
SELECT 
    [Your_Dimension],
    SUM(Sales) as Total_Sales,
    SUM(Profit) as Total_Profit,
    COUNT(*) as Transaction_Count,
    AVG(Profit / Sales) * 100 as Avg_Margin
FROM Global_Superstore_Clean
WHERE [Your_Conditions]
GROUP BY [Your_Dimension]
ORDER BY Total_Profit DESC;
```

## Data Quality Validation

### Automated Checks
```sql
-- Check data completeness
SELECT 
    'Orders' as Table_Name,
    COUNT(*) as Total_Records,
    COUNT(CASE WHEN Order_Date IS NULL THEN 1 END) as Missing_Dates,
    COUNT(CASE WHEN Customer_ID IS NULL THEN 1 END) as Missing_Customers,
    COUNT(CASE WHEN Sales <= 0 THEN 1 END) as Invalid_Sales
FROM Global_Superstore_Clean;

-- Business logic validation
SELECT 
    'Date Consistency' as Validation_Check,
    COUNT(*) as Violations
FROM Global_Superstore_Clean
WHERE Ship_Date < Order_Date;
```

## Troubleshooting

### Common Issues
1. **Slow Queries:** Check indexes and query structure
2. **Incorrect Results:** Validate business logic and data types
3. **Memory Issues:** Process data in batches for large datasets
4. **Connection Problems:** Verify database credentials and permissions

### Debugging Tips
- Use EXPLAIN PLAN to analyze query performance
- Validate intermediate results step by step
- Check data types and format consistency
- Test with sample data before full execution
