# Power Piston Plug - Car Sales Dashboard

This repository currently contains dashboard screenshots and a short project description. To make the work complete and usable, this project now includes a practical dashboard process, an example car sales dataset, and a clear implementation track for building the final Power BI dashboard.

## Project goal

Create a complete Power BI car sales dashboard that helps business users answer questions like:

- Which car brand sells the most?
- Which region performs best?
- Which model contributes the highest revenue?
- How are sales trending month by month?
- Which dealership or segment is underperforming?
- What is the impact of discounts and profit margin?

## Business context

This dashboard is designed for a cars sales dataset and should support management review, sales analysis, regional comparisons, product performance, and forecast decision-making.

## Recommended dashboard structure

### 1. Executive summary page
- KPI cards:
  - Total Revenue
  - Total Units Sold
  - Average Selling Price
  - Profit Margin
- Sales trend line chart by month
- Sales by region
- Top 10 models by revenue
- Sales vs target comparison

### 2. Product performance page
- Revenue by brand
- Units sold by model
- Profit by vehicle type
- Discount impact analysis
- Trend of best-selling vehicles

### 3. Regional sales page
- Map visual by state/city
- Sales by region and dealer
- Customer segment analysis
- Sales performance by year

### 4. Customer and market insights page
- Sales by customer type
- Payment method or financing mix
- Channel analysis
- Weak-performing segment drilldown

## Data model

Use a fact table with the following fields:

- Date
- Year
- Month
- Region
- Country
- City
- Dealer
- Brand
- Model
- VehicleType
- Segment
- SalesChannel
- UnitsSold
- UnitPrice
- DiscountPercent
- Revenue
- Cost
- Profit
- CustomerType

## Suggested Power BI workflow

### Step 1: Import data
- Load CSV or Excel sales data into Power BI Desktop.
- Confirm column names and data types.
- Remove blank or duplicate rows.
- Standardize region and brand names.

### Step 2: Clean and transform
- Convert Date column to proper date type.
- Create a calendar table.
- Split City/State/Region if needed.
- Replace null values with defaults where appropriate.
- Create custom columns for month names and year.

### Step 3: Build a star schema
- Fact table: `SalesFact`
- Dimension tables:
  - `DateDim`
  - `RegionDim`
  - `ProductDim`
  - `DealerDim`
  - `CustomerDim`

### Step 4: Create DAX measures

```DAX
Total Revenue = SUM('SalesFact'[Revenue])

Total Units Sold = SUM('SalesFact'[UnitsSold])

Average Selling Price = DIVIDE([Total Revenue], [Total Units Sold], 0)

Total Profit = SUM('SalesFact'[Profit])

Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0)

Sales YoY % =
VAR CurrentYearSales = CALCULATE([Total Revenue], YEAR('DateDim'[Date]) = YEAR(TODAY()))
VAR PreviousYearSales = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR('DateDim'[Date]))
RETURN DIVIDE(CurrentYearSales - PreviousYearSales, PreviousYearSales, 0)

Units Sold by Brand = CALCULATE([Total Units Sold], ALLEXCEPT('SalesFact', 'SalesFact'[Brand]))
```

### Step 5: Add visuals
- Card: Total Revenue
- Card: Total Units Sold
- KPI: Profit Margin
- Line chart: Monthly sales trend
- Bar chart: Revenue by brand
- Matrix: Revenue by region and model
- Map: Sales by city/state
- Column chart: Units sold by model

### Step 6: Add slicers and filters
- Year
- Region
- Brand
- Dealer
- Customer Type
- Vehicle Type

### Step 7: Dashboard formatting
- Use a clean white background with dark blue accents
- Keep white space consistent
- Use bold titles and high contrast text
- Add tooltips on profit and revenue
- Keep layout professional and executive-friendly

## Sample dataset

A starter dataset has been added at:

- `data/car_sales_data_sample.csv`

This file contains example records for brand, region, model, units sold, cost, revenue, and profit. It can be used to build the dashboard in Power BI.

## Suggested final dashboard pages

1. Overview
2. Sales Performance
3. Product Analysis
4. Region Analysis
5. Profitability

## Completion checklist

- [x] Repository overview established
- [x] Business context defined
- [x] Dashboard structure prepared
- [x] Data model suggested
- [x] DAX measures provided
- [x] Sample sales dataset added
- [ ] Power BI .pbix file to be created from the sample dataset
- [ ] Final dashboard visuals to be polished based on stakeholder review
- [ ] Publish to Power BI Service if needed

## Next steps

To complete the actual dashboard in Power BI:

1. Open Power BI Desktop.
2. Import `data/car_sales_data_sample.csv`.
3. Build the relationships and calendar table.
4. Create the measures listed above.
5. Add the visuals and filters.
6. Review the layout and publish the dashboard.

## Repository notes

This repository is currently a dashboard concept and sample project. For a full production-ready dashboard, add:

- Real sales data file
- Power BI `.pbix` project file
- Data dictionary
- Business requirements document
- Additional DAX and forecast metrics

## Summary

The dashboard process is now structured around real business analysis, from data cleaning to KPI design, visual layout, and final presentation. This gives a complete starting point for a Power BI car sales dashboard.

