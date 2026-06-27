# Sales Performance Dashboard using Tableau

## Business Problem Summary

The objective of this project is to develop an executive Tableau dashboard that enables business stakeholders to monitor overall sales performance, profitability, regional performance, customer segments, and shipping methods. The dashboard provides interactive insights to support data-driven business decisions.

---

## Dataset Description

The project uses a retail sales dataset containing transactional information, including:

* Order Date
* Sales
* Profit
* Region
* Category
* Customer Segment
* Ship Mode
* Customer Rating
* Product Information
* Discount
* Quantity

The dataset was provided as an Excel (.xlsx) file.

---

## Tableau Workbook Description

The Tableau workbook **Sales_Performance_Dashboard.twbx** contains an executive dashboard consisting of KPI cards, trend analysis, profitability analysis, customer segmentation, and shipping performance. Interactive filters allow users to explore the data dynamically.

---

## Calculated Fields Created

The following calculated fields were used:

* Total Sales
* Total Profit
* Total Orders (COUNTD of Order ID)
* Average Customer Rating

---

## Dashboard Components

The dashboard includes:

* Total Sales KPI
* Total Profit KPI
* Total Orders KPI
* Average Customer Rating KPI
* Sales Trend View
* Regional Performance View
* Category Profitability View
* Customer Segment View
* Ship Mode Distribution

---

## Filters and Interactions Used

Interactive Filters:

* Region
* Category
* Customer Segment

Dashboard Interaction:

* Selecting a region filters the remaining dashboard views.
* Filters update all charts dynamically for interactive analysis.

---

## Key Business Insights

* Sales remain relatively consistent throughout the year.
* South region records the highest sales performance.
* Technology is the most profitable category.
* Home Office customers generate the highest sales.
* Standard Class is the most frequently used shipping mode.
* Regional performance varies significantly across markets.
* Executive KPIs provide a quick overview of business performance.
* Interactive filters enable detailed business analysis.

---

## Dashboard Story Summary

The dashboard presents an executive overview of business performance by combining sales trends, regional analysis, profitability, customer behavior, and shipping patterns into a single interactive view. Decision-makers can quickly identify high-performing regions and categories while exploring detailed trends using filters.

---

## Assumptions and Limitations

### Assumptions

* Dataset is complete and accurate.
* Customer ratings are correctly recorded.
* Sales and profit values are reported without duplication.

### Limitations

* Analysis is limited to the available dataset.
* External business factors such as seasonality and market conditions are not included.
* No predictive or forecasting analysis has been performed.

---

## Screenshots Included

* full_dashboard.png
* sales_trend_view.png
* regional_performance_view.png
* category_profitability_view.png
* filter_interaction_view.png

---

## Repository Structure

```
data/
outputs/
screenshots/
tableau/
README.md
```
