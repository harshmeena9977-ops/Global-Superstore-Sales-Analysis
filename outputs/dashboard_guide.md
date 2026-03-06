# Power BI Dashboard User Guide

## Dashboard Overview

### Dashboard Files
- **Sales_Analysis.pbix** - Main interactive Power BI dashboard
- **Overview.png** - Sales & profitability overview screenshot
- **Furniture.png** - Furniture margin optimization analysis
- **Customer.png** - Customer profitability & shipping efficiency
- **Map.png** - Regional profitability geographic visualization

## Dashboard Navigation

### Page 1: Sales & Profitability Overview
**Purpose:** Executive-level view of overall business performance

#### Key Metrics
- **Total Sales:** Revenue across all categories and regions
- **Total Profit:** Net profitability after discounts and costs
- **Profit Margin:** Overall profit percentage (target: >30%)
- **YoY Growth:** Year-over-year performance comparison

#### Visualizations
- **Sales Trend Chart:** Monthly revenue from 2011-2014
- **Category Performance:** Bar chart of sales by product category
- **Regional Map:** Geographic distribution of profits
- **KPI Cards:** Key performance indicators with trend arrows

#### Interactive Features
- **Year Slicer:** Filter data by specific year (2011-2014)
- **Category Filter:** Focus on specific product categories
- **Region Slicer:** Analyze specific geographic regions

### Page 2: Furniture Margin Optimization
**Purpose:** Detailed analysis of furniture category profitability

#### Key Insights
- **Discount Impact:** How different discount levels affect margins
- **Sub-Category Analysis:** Performance by furniture sub-categories
- **Marginal Analysis:** Break-even points and optimal pricing

#### Visualizations
- **Discount vs. Profit Scatter:** Relationship between discounts and profitability
- **Sub-Category Bar Chart:** Performance comparison across furniture types
- **Margin Trend Line:** Margin changes over time by discount level
- **Risk Matrix:** High/low margin product identification

#### Critical Finding
- **25% Discount Threshold:** Margins become negative when discounts exceed 25%
- **Tables Sub-Category:** Highest risk category for margin erosion

### Page 3: Customer Profitability & Shipping Efficiency
**Purpose:** Customer segmentation and operational efficiency analysis

#### Customer Analytics
- **Top Customers:** Highest value customers by profit contribution
- **Customer Segments:** B2B vs. B2C performance comparison
- **Customer Lifetime Value:** Long-term customer profitability

#### Shipping Analysis
- **Shipping Mode Performance:** Profitability by shipping method
- **Delivery Time Analysis:** Speed vs. cost trade-offs
- **Regional Shipping:** Geographic shipping efficiency

#### Visualizations
- **Customer Profitability Chart:** Top 20 customers by profit
- **Shipping Mode Comparison:** Profit and efficiency metrics
- **Customer Segments Pie:** B2B vs. B2C distribution
- **Shipping Efficiency Matrix:** Cost vs. delivery time analysis

## Interactive Features

### Slicers & Filters
- **Time Filters:** Year, quarter, month selection
- **Geographic Filters:** Country, state, city selection
- **Product Filters:** Category, sub-category selection
- **Customer Filters:** Segment, value tier selection

### Drill-Down Capabilities
- **Category → Sub-Category:** Drill from product categories to specific items
- **Country → State → City:** Geographic hierarchy navigation
- **Customer → Orders:** Individual customer transaction details

### Cross-Filtering
- **Automatic Filtering:** Selections update all related visuals
- **Highlighting:** Hover effects show detailed information
- **Tooltips:** Rich tooltips with additional context and metrics

## Business Intelligence Features

### KPI Calculations
```dax
// Key Performance Indicators
Total Sales = SUM(Sales[Sales])
Total Profit = SUM(Sales[Profit])
Profit Margin % = DIVIDE([Total Profit], [Total Sales]) * 100
YoY Growth = DIVIDE(CurrentYear - PreviousYear, PreviousYear)

// Advanced Metrics
High Discount Impact = CALCULATE([Total Profit], Sales[Discount] > 0.25)
Customer Lifetime Value = CALCULATE([Total Sales], ALLSELECTED(Customer))
Shipping Efficiency = DIVIDE([Total Profit], COUNTROWS(Orders))
```

### Conditional Formatting
- **Profit Margins:** Color-coded (green >30%, yellow 20-30%, red <20%)
- **Growth Indicators:** Arrows showing positive/negative trends
- **Risk Levels:** Visual indicators for high-discount products

### Tooltips & Details
- **Rich Tooltips:** Additional metrics on hover
- **Drill-Through:** Navigate to detailed analysis
- **Data Labels:** Key values displayed on charts

## Performance & Optimization

### Loading Performance
- **Initial Load:** ~15 seconds for full dataset
- **Filter Response:** <2 seconds for slicer interactions
- **Drill-Down:** <3 seconds for detailed views

### Memory Optimization
- **Data Model:** Star schema for optimal performance
- **Measures:** Pre-calculated for faster rendering
- **Visuals:** Optimized for clarity and speed

### Best Practices
- **Visual Hierarchy:** Most important metrics prominently displayed
- **Color Consistency:** Consistent color scheme across pages
- **Responsive Design:** Works on different screen sizes

## Usage Scenarios

### Executive Dashboard
1. Open Page 1 for overall business overview
2. Use Year slicer to compare performance
3. Review KPI trends and regional performance
4. Export summary reports for board meetings

### Category Manager Analysis
1. Navigate to Page 2 for detailed category analysis
2. Filter to specific product categories
3. Analyze discount impact on margins
4. Identify optimization opportunities

### Customer Relationship Management
1. Use Page 3 for customer insights
2. Filter to high-value customer segments
3. Analyze shipping efficiency by customer type
4. Develop targeted retention strategies

## Export & Sharing

### Export Options
- **PDF Export:** File → Export → Create PDF
- **Image Export:** Right-click visual → Copy image
- **Data Export:** Right-click visual → Export data
- **Print:** File → Print → Select destination

### Sharing Options
- **Power BI Service:** Publish for team collaboration
- **Web Embed:** Generate embed code for websites
- **Email Subscription:** Schedule automated reports
- **Link Sharing:** Share dashboard with stakeholders

### Customization Guide
- **Color Schemes:** Modify theme colors in Power BI
- **Logos:** Add company branding to headers
- **Layouts:** Rearrange visuals for specific needs
- **New Measures:** Add custom KPIs as needed

## Troubleshooting

### Common Issues
- **Slow Loading:** Check data source connections and model size
- **Incorrect Data:** Verify data refresh and source file integrity
- **Filter Not Working:** Check slicer configuration and data types
- **Visual Errors:** Validate measure calculations and relationships

### Performance Tips
- **Reduce Data Volume:** Use filters for large datasets
- **Optimize Measures:** Simplify complex DAX calculations
- **Visual Cleanup:** Remove unnecessary visuals
- **Data Model:** Optimize relationships and cardinality

### Support Resources
- **Documentation:** Review technical documentation
- **Community:** Power BI community forums
- **Training:** Microsoft Power BI learning resources
- **Support:** Contact IT for data source issues
