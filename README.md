# Global Superstore Sales Analysis

An independent analytics practice project using a retail transaction dataset. It explores sales and profit by category, region, customer segment, discount, and shipping mode through SQL analysis and a Power BI report. This is a portfolio exercise; it was not commissioned by or delivered to a company, and the findings are not measured business impact.

## Project artifacts

- [Open the Power BI report](outputs/Sales_Analysis.pbix)
- [View the overview screenshot](outputs/Overview.png.png)
- [View the furniture analysis screenshot](outputs/Furniture.png.png)
- [View the customer analysis screenshot](outputs/Customer.png.png)
- [View the regional map screenshot](outputs/Map.png.png)
- [Browse SQL analysis queries](docs/Cleaning_Modeling.sql.txt)
- [Open the executed analysis notebook](scripts/sales_performance_sql%20(1).ipynb)
- [Read the Power BI measures notes](docs/measures.md.txt)
- [Read the dashboard guide](outputs/dashboard_guide.md)

## Questions explored

The analysis files contain queries and saved notebook outputs for:

- Comparing sales and profit by category, sub-category, region, and customer segment.
- Reviewing discount levels alongside profit.
- Listing products and customers by profit.
- Comparing sales and profit by shipping mode.
- Reviewing monthly and quarterly patterns.

These are descriptive comparisons in the included dataset. They do not establish that a discount threshold causes a change in profit, or that a recommendation would improve a real business outcome. Numerical findings from older project notes have been omitted here until they are reconciled against the source data and the Power BI report.

## Data and limitations

The repository includes a CSV file at data/Global_Superstore2.csv and an Excel workbook at data/Cleaned_data.csv.xlsx. The original publisher, source URL, version, and dataset reuse terms are not documented in this repository. The project license at docs/LICENSE does not establish rights to redistribute the dataset.

The notebook contains saved results, but the repository does not yet provide a verified, end-to-end setup that recreates the database, imports the CSV, and runs every query from a clean environment. Treat the saved outputs as project artifacts pending that reproducibility check. Do not assume older row-count, geography, or metric claims are validated.

## Repository layout

- data/ — source-named CSV and processed Excel workbook.
- docs/ — SQL query file, analysis notes, DAX notes, technical notes, and project license.
- outputs/ — Power BI report, screenshots, and dashboard guide.
- scripts/ — Jupyter notebook and supporting notes.

## Review the report

Download outputs/Sales_Analysis.pbix and open it in Power BI Desktop. The repository also includes four report screenshots for quick review. A live hosted dashboard is not provided. If Power BI asks for a data source path, point it to the included CSV or workbook and verify the report refresh before relying on its numbers.

## Reproducibility status

The repository contains analysis artifacts, but a clean-run setup is not documented yet. Before treating the notebook outputs or report metrics as reproducible, document the database/engine and version, dataset import steps, file paths, required packages, and a fresh-run validation procedure. The SQL file includes queries but does not provide a complete database creation and loading script.

## Tools evidenced in the repository

- SQL query files and SQL-oriented notebook analysis.
- Power BI report and DAX measure notes.
- CSV and Excel data files.

No SQL Server requirement is stated here because the repository does not include a verified SQL Server setup. The code, data, and dashboard have not been changed as part of this README update.
