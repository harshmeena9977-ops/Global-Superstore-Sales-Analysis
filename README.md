# 🏪 Global Superstore Sales Analytics Dashboard

## 📊 Problem Statement
Global Superstore, a multinational retail corporation, needed actionable insights to optimize profitability across diverse product categories, regions, and customer segments. The company faced challenges with margin erosion, inefficient discount strategies, and lacked data-driven visibility into shipping and customer performance metrics.

## 🗄️ Dataset Overview
**Source:** Global Superstore retail transaction data  
**Size:** 12.1MB (10,000+ records)  
**Time Period:** 2011-2014 (4 years of retail operations)  
**Geography:** 50+ countries across 5 continents  

### Key Features:
- **Sales Data:** Revenue, profit, discount percentages, quantity sold
- **Product Hierarchy:** Categories (Furniture, Office Supplies, Technology) and sub-categories
- **Customer Analytics:** Customer segments, purchase patterns, profitability metrics
- **Operational Data:** Shipping modes, order dates, regional performance
- **Geographic Information:** Country, state, city mapping for location analysis

## 🔬 Approach & Methodology

### 1. Data Cleaning & Preparation
- **Data Validation:** Removed duplicate orders and corrected missing values
- **Feature Engineering:** Created profit margins, discount impact ratios
- **SQL Transformation:** Cleaned and structured data using complex queries

### 2. Business Intelligence Development
- **Multi-Page Dashboard Architecture:** 3 focused analytical modules
- **KPI Framework:** 20+ key performance indicators with drill-down capabilities
- **Interactive Slicers:** Year, region, segment, category, and shipping filters

### 3. Advanced Analytics Implementation
- **Profitability Analysis:** Category and regional profit contribution
- **Discount Optimization:** Identified 25% discount threshold for margin protection
- **Customer Segmentation:** High-value customer identification and retention strategies

## 🛠️ Tools & Technologies

| Category | Tools | Purpose |
|----------|-------|---------|
| **Database** | SQL Server | Data cleaning, validation, KPI calculations |
| **Analytics** | SQL, Excel | Data transformation and analysis |
| **Visualization** | Power BI | Interactive dashboards, geographic mapping |
| **Documentation** | Markdown | Technical documentation and insights |

## 💡 Key Insights & Business Impact

### Revenue Optimization
- **Technology Category:** $664K profit with highest margins (45% avg)
- **Furniture Margin Alert:** Losses occur when discounts exceed 25%
- **Regional Performance:** APAC region shows 23% higher profit margins

### Operational Efficiency  
- **Shipping Optimization:** Standard Class generates $891K profit (most efficient)
- **Customer Profitability:** Top 10 customers contribute 20%+ of total margin
- **Discount Strategy:** Identified optimal discount ranges by product category

### Strategic Recommendations
- **Margin Protection:** Cap furniture discounts at 25% threshold
- **Customer Retention:** Focus on high-value customers like Tamara Chand ($8.7K margin)
- **Shipping Strategy:** Promote Standard Class for cost efficiency

## 📈 Visualizations & Dashboards

### Dashboard Modules
1. **Sales & Profitability Overview:** Revenue trends, category performance
2. **Furniture Margin Optimization:** Discount impact analysis  
3. **Customer Profitability & Shipping Efficiency:** Customer segmentation

### Key Visual Elements
- **Geographic Maps:** Regional profit distribution across 50+ countries
- **Trend Analysis:** Year-over-year performance tracking
- **Profit Margin Charts:** Category and sub-category profitability
- **Customer Analytics:** High-value customer identification

## 🚀 How to Run This Project

### Prerequisites
```bash
# Install Power BI Desktop
# Install SQL Server (for data processing)
# Clone repository
```

### Setup Instructions
```bash
# 1. Clone repository
git clone https://github.com/harshmeena9977-ops/Global-Superstore-Sales-Analysis.git
cd Global-Superstore-Sales-Analysis

# 2. Open Power BI Dashboard
# Open Sales_Analysis.pbix in Power BI Desktop

# 3. Explore Interactive Features
# Use slicers for Year, Region, Segment, Category filtering
# Navigate between 3 dashboard pages
# Export insights using built-in Power BI features
```

### Data Processing
```sql
-- Key SQL transformations available in:
-- scripts/Cleaning_Modeling.sql.txt

-- Sample profit margin calculation:
SELECT 
    Category,
    SUM(Profit) / SUM(Sales) * 100 as Profit_Margin,
    SUM(Sales) as Total_Revenue,
    SUM(Profit) as Total_Profit
FROM Global_Superstore2
GROUP BY Category;
```

## 📋 Project Structure
```
├── README.md                    # This file
├── Sales_Analysis.pbix          # Main Power BI dashboard
├── Global_Superstore2.csv       # Raw dataset
├── Cleaned_data.csv.xlsx        # Processed clean data
├── sales_performance_sql.ipynb  # SQL analysis notebook
├── Cleaning_Modeling.sql.txt    # Data transformation scripts
├── insights.md.txt              # Key business findings
├── measures.md.txt              # Power BI measure definitions
└── Dashboard Screenshots/       # Visual outputs
    ├── Overview.png
    ├── Furniture.png
    ├── Customer.png
    └── Map.png
```

## 🏆 Resume Achievement

**Senior Data Analyst** | Global Superstore Sales Analytics  
*Developed comprehensive retail analytics dashboard analyzing 10K+ transactions across 50+ countries, identifying 25% discount optimization threshold that prevented margin erosion and enabled data-driven pricing strategies*

## 📞 Contact & Repository
- **GitHub:** [harshmeena9977-ops/Global-Superstore-Sales-Analysis](https://github.com/harshmeena9977-ops/Global-Superstore-Sales-Analysis)
- **Live Dashboard:** Available in Sales_Analysis.pbix
- **Dataset Source:** Global Superstore synthetic retail data

---

*Last Updated: March 2026 | Project Version: 2.0 (Recruiter-Ready)*
