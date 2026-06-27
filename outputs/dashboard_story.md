# Dashboard Story — Sales Performance Dashboard
**Student:** Priya Singh | **ID:** 2511034  
**Workbook:** Sales_Performance_Dashboard.twbx  
**Tool:** Tableau Desktop 2026.2  
**Dataset:** dashboard_sales_data.xlsx (4,200 orders, Jan 2024 – Dec 2025)

---

## Overview

This dashboard tells the story of a retail business's performance across two full years through a single interactive executive view titled **"Sales Performance Dashboard."** It combines four KPI metric cards at the top with five analytical charts below, all connected through a Region-based dashboard action that allows leadership to drill into any geography instantly.

---

## Act 1 — The Headline Numbers (KPI Cards)

Before examining any chart, a business leader opening this dashboard immediately sees **four KPI metric cards** arranged across the top row:

| KPI Card | What It Shows |
|---|---|
| **Total Sales** | Aggregate revenue across all 4,200 orders, displayed in millions (e.g., "217.02M") |
| **Total Profit** | Total profit across all orders, displayed in millions |
| **Total Orders** | Count of distinct order IDs — 4,200 unique orders |
| **Average Rating** | Mean customer satisfaction score across all orders |

These four numbers tell the complete business health story in under five seconds: *How much did we sell? How much did we make? How many customers served? Are they happy?*

All four KPI cards are connected to the **Region dashboard action** — when a leader clicks on a region in the Regional Performance chart, all four KPIs instantly recalculate to show only that region's figures. This makes the cards dynamic, not static.

---

## Act 2 — Are We Growing? (Sales Trend View)

**Chart:** Sales Trend View — Line Chart  
**Dimensions:** Month on the x-axis, Total Sales on the y-axis  
**Filters applied:** Region filter (driven by dashboard action), Customer Segment filter (driven by shared view filter)

The Sales Trend line chart is positioned as the first major chart below the KPI row, spanning the full width of the dashboard. It answers the fundamental question: *Is revenue going in the right direction?*

The chart plots monthly sales aggregated from `order_date` across the full January 2024 to December 2025 period, giving 24 data points. Key observations visible in this view:

- **2025 slightly outperformed 2024** — total 2025 sales of approximately ₹11.08 Crore compared to ₹10.62 Crore in 2024, showing a positive 4.3% year-on-year trend.
- **Visible seasonality** — peaks are visible in Q1 (January–February) and Q4, with a mid-year trough typically in May–July.
- **No catastrophic dips** — no month shows a revenue collapse, confirming operational stability across the period.

The chart responds to both the Region dashboard action and the Customer Segment filter (Consumer, Corporate, Home Office). When a leader selects "South" region in the Regional Performance chart, the Sales Trend instantly redraws to show only the South region's monthly trajectory.

**Business Story:** The business is growing, but the seasonal pattern is consistent and predictable. Leadership should plan inventory and marketing campaigns before known peak periods.

---

## Act 3 — Where Are We Winning? (Regional Performance View)

**Chart:** Regional Performance View — Vertical Bar Chart  
**Dimensions:** Region on the x-axis (sorted descending by Sales), Total Sales on the y-axis  
**Colour encoding:** Sum of Profit (sequential colour scale — higher profit = darker colour)  
**Filter:** Region filter (user-selectable from right-side panel)

The Regional Performance bar chart is positioned in the lower section of the dashboard and serves a dual purpose: it is both a standalone chart *and* the primary filter driver for the entire dashboard. Clicking any region bar activates a **dashboard action** that filters every other sheet simultaneously.

Sales by region rank as follows:
| Region | Sales | Colour Intensity |
|---|---|---|
| South | Highest | Darkest (highest profit) |
| North | Second | Medium |
| West | Third | Medium-light |
| East | Lowest | Lightest |

The colour encoding by profit reveals whether high-sales regions are also high-profit regions — a critical strategic insight. A region with tall bars but light colour would signal volume without margin, a warning sign.

**Dashboard Action:** Clicking "South" in this chart immediately updates all five other charts and all four KPI cards to show South-only data. This single click transforms the entire dashboard into a regional deep-dive without any manual filtering.

**Business Story:** The South region leads in both revenue and profitability. The dashboard action allows South's Regional Manager to review their own Sales Trend, Category mix, Customer Segment split, and Shipping distribution in one click.

---

## Act 4 — What Is Making Money? (Category Profitability View)

**Chart:** Category Profitability View — Horizontal Bar Chart  
**Dimensions:** Category on the y-axis (sorted descending by profit), Sum of Profit on the x-axis  
**Colour encoding:** Sum of Sales (sequential colour scale — higher sales = darker colour)  
**Filters:** Category filter (user-selectable), Region filter (driven by dashboard action)

The Category Profitability chart answers: *Which product lines are generating profit, and how does that relate to their sales volume?*

The three categories sort as follows by profit:
| Category | Profit | Sales Colour |
|---|---|---|
| Technology | Highest profit | Darkest (highest sales) |
| Furniture | Second | Medium |
| Office Supplies | Lowest | Lightest |

The dual encoding — profit on the x-axis length, sales as colour — immediately reveals the relationship between revenue and profit at category level. Technology dominates both dimensions (18.2% margin, 70.9% of sales), while Furniture has significant sales but disproportionately low profit (6.9% margin).

The chart has both a **Category filter** on its right panel (allowing isolation of individual categories) and responds to the **Region dashboard action**, meaning a leader can ask: "What is Furniture's profitability contribution in just the East region?"

**Business Story:** Technology is the profit engine. Furniture needs urgent margin analysis. The colour encoding makes the category-level sales/profit relationship immediately visible without reading any numbers.

---

## Act 5 — Who Is Buying From Us? (Customer Segment View)

**Chart:** Customer Segment View — Horizontal Bar Chart  
**Dimensions:** Customer Segment on the y-axis (sorted descending by sales), Total Sales on the x-axis  
**Colour encoding:** Sum of Profit  
**Axis label:** "Total Sales" (custom axis title)  
**Filter:** Customer Segment filter (user-selectable from right panel)

The Customer Segment chart shows revenue distribution across the three customer types: **Home Office**, **Consumer**, and **Corporate**.

The three segments are remarkably balanced — within approximately 2 percentage points of each other in sales contribution (Home Office ≈34.3%, Consumer ≈33.1%, Corporate ≈32.5%). This near-perfect balance is itself a strategic insight — the business is not dangerously dependent on any single customer type.

The profit colour encoding adds a second layer: are higher-sales segments also more profitable? This allows leadership to compare not just revenue volume but profit quality across segments.

**Business Story:** The balanced segment split is a business strength. Combined with the Customer Segment filter on this sheet, leadership can isolate any single segment and review its contribution in context of the region and date filters already applied.

---

## Act 6 — How Are Orders Being Shipped? (Ship Mode Distribution)

**Chart:** Ship Mode Distribution — Horizontal Bar Chart  
**Dimensions:** Ship Mode on the y-axis (sorted descending by sales), Total Sales on the x-axis  
**Colour encoding:** Sum of Profit  
**Axis label:** "Total Sales" (custom axis title)  
**Filter:** Responds to Region dashboard action

The Ship Mode Distribution chart answers: *How are our orders being fulfilled, and are premium shipping options generating better margins?*

Ship modes sorted by sales:
| Ship Mode | Sales Share | Notes |
|---|---|---|
| Standard Class | ~56.5% | Most common mode |
| Second Class | ~22.0% | Second most common |
| First Class | ~14.7% | Premium speed |
| Same Day | ~6.7% | Fastest, least common |

The profit colour encoding reveals whether premium shipping modes (Same Day, First Class) are associated with higher-margin orders — they typically are, as they correlate with Technology orders where customers prioritise speed.

**Business Story:** Standard Class dominates volume but leadership should monitor whether the delivery SLA (3–5 days) is being met. The dashboard action means this chart updates when a region is selected, allowing logistics managers to review shipping mode preferences by geography.

---

## How the Dashboard Connects — The Action Filter

The most powerful feature of this dashboard is the **Region dashboard action** attached to the Regional Performance View chart. This is defined in the workbook as `Action1_366EE664FA49473FBA3DBD125529D1AC`.

**How it works:**
1. Leader opens the "Executive Dashboard" tab
2. All charts show full dataset across all regions
3. Leader clicks on the **"South"** bar in the Regional Performance chart
4. **Instantly**, all other sheets update:
   - Sales Trend shows only South monthly sales
   - Category Profitability shows South category profits
   - Customer Segment shows South customer revenue
   - Ship Mode shows South shipping distribution
   - All four KPI cards recalculate for South only
5. Leader clicks again (or clicks on a blank area) to clear the filter and return to the full view

**To clear the filter:** Click on an empty area of the Regional Performance chart, or click the same region again.

This single interaction pattern allows a complete regional review without touching any filter panel — the chart itself is the navigation.

---

## The Complete Dashboard Story in One Paragraph

The Sales Performance Dashboard opens with four headline numbers confirming a healthy, growing business: strong total sales, a solid profit figure, 4,200 orders served, and satisfied customers with a rating above 4. The Sales Trend chart confirms consistent growth with predictable seasonality. The Regional Performance chart — the interactive centre of the dashboard — reveals South as the leading region, and a single click on any region rebuilds every other view instantly. Below, the Category Profitability chart confirms Technology as the profit engine while flagging Furniture's margin challenge. The Customer Segment and Ship Mode charts complete the picture, showing a well-balanced customer base and Standard Class as the dominant fulfilment mode. Every chart, every KPI, every filter is connected — this is not five separate charts but one unified analytical story.

---

*This story document is based on analysis of Sales_Performance_Dashboard.twbx built in Tableau Desktop 2026.2.*  
*Part 4 — Business Analytics Assignment | Student: Priya Singh | ID: 2511034*
