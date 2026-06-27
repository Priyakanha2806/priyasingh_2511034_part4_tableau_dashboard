# Chart Selection Justification
**Student:** Priya Singh | **ID:** 2511034  
**Dashboard:** Sales Performance Dashboard (Sales_Performance_Dashboard.twbx)  
**Tool:** Tableau Desktop 2026.2  
**Date:** June 2025

---

## Overview

This document justifies every chart type, encoding choice, and design decision in the Sales Performance Dashboard. Each chart was evaluated against three criteria:

1. **Question clarity** — Does this chart type answer the intended business question most directly?
2. **Data structure fit** — Is this chart appropriate for the variables being compared (categorical vs continuous, one measure vs two, ranking vs trend)?
3. **Audience accessibility** — Is this chart readable by a non-technical executive without explanation?

The dashboard contains five worksheet-level charts and four KPI metric cards across the "Executive Dashboard" view.

---

## 1. KPI Cards — Total Sales, Total Profit, Total Orders, Average Rating

**Sheet names:** Total Sales, Total Profit, Total Orders, Average Rating  
**Mark type:** Text (number displayed in bold, font size 28)  
**Variables:** Single aggregate measure per card

### Why KPI Text Cards?

KPI cards display a single large number — the maximum possible reduction of a dataset to a single meaningful figure. They are not charts in the traditional sense; they are **decision anchors**.

The four metrics chosen cover the complete business performance spectrum:
- **Total Sales** — revenue volume (how big is the business?)
- **Total Profit** — financial outcome (is the business making money?)
- **Total Orders** — operational volume (how many customers served?)
- **Average Rating** — customer experience (are customers satisfied?)

No other chart type could communicate these four figures with equal clarity in the same screen space. A bar chart or line chart showing the same data would require the viewer to read axes, interpret scales, and mentally aggregate — adding cognitive load to a number that should be instantly readable.

### Why These Four Metrics Specifically?

These four KPIs were selected because each answers a different dimension of business performance that the other three cannot substitute for:
- Sales without profit is incomplete (a company can sell a lot but lose money)
- Profit without orders is incomplete (a high margin on very few orders may not be sustainable)
- Orders and sales without customer rating is incomplete (a business growing through dissatisfied customers is fragile)

### Dynamic Behaviour

Critically, all four KPI cards are connected to the Region dashboard action. When a user clicks "South" in the Regional Performance chart, all four cards recalculate immediately for South alone. This transforms the cards from static summaries into live regional scorecards — the same four cards serve as the headline KPIs for the whole business and as the regional performance overview simultaneously.

### Design Choice — Bold Font Size 28

The workbook specifies font size 28 bold for all KPI card values. This is a deliberate readability choice: the number must be legible from across a meeting room screen. Supporting context (the card title, format suffix like "M" for millions) is displayed smaller. The hierarchy of font size encodes the hierarchy of importance: the number matters most.

---

## 2. Sales Trend View — Line Chart

**Sheet name:** Sales Trend View  
**Mark type:** Line (Automatic)  
**Variables:** Month of Order Date (x-axis, ordinal) × Sum of Sales (y-axis, continuous)  
**Filters:** Region (dashboard action), Customer Segment (shared view filter), Region (additional)

### Why a Line Chart?

A line chart is the only appropriate chart type for **continuous time-series data**. The key properties that make it correct here:

1. **Temporal ordering** — months have a natural left-to-right sequence; the line visually encodes the direction of change
2. **Continuity** — monthly sales are samples from a continuous process; the connecting line implies the values between data points
3. **Trend visibility** — the slope of the line communicates growth or decline instantaneously; no axis reading is required to perceive direction
4. **Pattern recognition** — repeating seasonal patterns (Q1 peaks, mid-year troughs) are immediately visible as recurring shapes in the line

### Why Monthly Granularity?

The workbook aggregates to Month (not Day or Year). This is the optimal granularity for executive-level trend analysis:
- **Daily** data would produce a jagged, noisy line with 730+ data points — too much detail for strategic decision-making
- **Yearly** data would show only 2 points — too little information to identify seasonal patterns
- **Monthly** data provides 24 data points — enough to show trend direction, identify seasonality, and spot anomalies, without overwhelming visual noise

### Alternatives Considered and Rejected

| Alternative | Why Rejected |
|---|---|
| Bar chart | Better for comparing discrete categories; harder to read trend direction at a glance; does not show seasonal shape clearly |
| Area chart | Works well for single-series data but creates clutter if multiple series overlap; line is cleaner for this use case |
| Scatter plot | Implies no relationship between adjacent time periods; removes the trend-reading advantage |
| Heat map (calendar) | Too operationally detailed for an executive view; appropriate for anomaly detection, not trend communication |

### Filter Interactions

The Sales Trend chart responds to two filters:
1. **Region dashboard action** — clicking a region bar in the Regional Performance chart filters the trend to show only that region
2. **Customer Segment shared filter** — the workbook defines a shared view that filters by Customer Segment across sheets

This means the trend line can be contextualised by any combination of region and customer segment, without adding visual complexity to the chart itself.

---

## 3. Regional Performance View — Vertical Bar Chart

**Sheet name:** Regional Performance View  
**Mark type:** Bar (Automatic)  
**Variables:** Region (x-axis, sorted descending by sales) × Sum of Sales (y-axis)  
**Colour encoding:** Sum of Profit (sequential colour scale)  
**Filter:** Region filter (available in right panel)  
**Role:** Primary dashboard action source

### Why a Vertical Bar Chart?

A vertical bar chart is the correct choice for **comparing a continuous measure across a small number of discrete categories**. The four regions (North, South, East, West) are a textbook use case: 4 categories, 1 measure to compare, ranking is the primary question.

Bar chart advantages for this data:
- Bar length directly encodes magnitude — no need to read numbers to compare bars
- Sorted descending order (South first) immediately answers "which region leads?"
- Vertical orientation suits the dashboard layout (wider than tall in this chart zone)

### Why Colour-Encode Profit?

The chart uses a sequential colour scale on Sum of Profit rather than Sum of Sales (which is already encoded in bar height). This adds a second dimension of insight without requiring a second chart: **Is the highest-sales region also the highest-profit region?**

A region with a tall bar (high sales) but light colour (low profit) would immediately signal a margin concern — the same insight that would require two separate charts if encoded differently.

### The Dashboard Action — Most Important Design Decision

The most significant design choice in this chart is that it serves as the **primary dashboard action source**. The action (`Action1`) is configured as:
- **Source:** Regional Performance View (this chart)
- **Target:** Executive Dashboard (all sheets)
- **Filter:** All fields (auto-clear when selection is removed)

This means clicking a region bar filters the entire dashboard. This design choice makes the Regional Performance chart the dashboard's navigation hub — not just a passive chart but an active filter control. The design principle is **chart-as-filter**: the most natural way to ask "show me only the South" is to click on "South" in the chart that shows regions.

### Alternatives Considered and Rejected

| Alternative | Why Rejected |
|---|---|
| Map/Filled map | India's state sizes do not proportionally represent sales contribution; a state with high sales but small geographic area would be visually underrepresented |
| Pie chart | Four nearly-equal segments (32–34% each) are harder to differentiate in a pie than in bars; also cannot encode a second measure (profit) without a second pie |
| Horizontal bar | Would also work; vertical was chosen to better suit the dashboard's wider-than-tall layout for this zone |
| Treemap | Better for hierarchical data; unnecessary complexity for a simple four-category comparison |

---

## 4. Category Profitability View — Horizontal Bar Chart

**Sheet name:** Category Profitability View  
**Mark type:** Bar (Automatic)  
**Variables:** Category (y-axis, sorted descending by profit) × Sum of Profit (x-axis)  
**Colour encoding:** Sum of Sales (sequential colour scale)  
**Filters:** Category filter (right panel), Region filter (dashboard action), Customer Segment (shared view)

### Why a Horizontal Bar Chart?

Category profitability requires a **ranking comparison** — which category generates the most profit? A horizontal bar chart is chosen over vertical for a practical reason: category names (Furniture, Office Supplies, Technology) are longer than region names and read naturally on a horizontal axis label without rotation.

The chart is sorted descending by profit, ensuring Technology (highest profit) appears at the top. This sort order means the most important information is always at the top-left of the viewer's natural reading pattern.

### Why Colour-Encode Sales?

The same dual-encoding rationale applies as in the Regional Performance chart: profit is encoded in bar length; sales volume is encoded in colour intensity. This lets the viewer instantly spot:
- **Long bar + dark colour** → high profit AND high sales (Technology — the ideal)
- **Medium bar + medium colour** → moderate profit, moderate sales (Furniture — concerning)
- **Short bar + light colour** → lower profit, lower sales (Office Supplies — smallest category)

Without the colour encoding, the chart would show only which category is most profitable by amount. With it, the chart also reveals whether the profit is proportionate to the sales volume — the margin relationship made visible.

### Why Not a Treemap or Stacked Bar?

| Alternative | Why Rejected |
|---|---|
| Treemap | Cannot represent negative profit values correctly (loss-making sub-categories would collapse to zero area); less intuitive for non-data audiences |
| Stacked bar | Harder to compare absolute profit heights between categories when bars are subdivided; the profit total per category is the primary question |
| Grouped bar | Would require a second Y-axis for profit percentage; adds complexity without proportionate benefit |

---

## 5. Customer Segment View — Horizontal Bar Chart

**Sheet name:** Customer Segment View  
**Mark type:** Bar (Automatic)  
**Variables:** Customer Segment (y-axis, sorted descending by sales) × Sum of Sales (x-axis, custom title "Total Sales")  
**Colour encoding:** Sum of Profit  
**Filter:** Customer Segment filter (right panel)

### Why a Horizontal Bar Chart (Again)?

The Customer Segment View uses the same chart type as Category Profitability for consistent design language: a horizontal bar with sales on the x-axis and profit as colour encoding. This consistency is intentional — both charts ask the same structural question ("how does [dimension] compare on [revenue] and [profit]?") and should use the same visual grammar.

The custom axis title "Total Sales" (instead of the default "SUM(sales)") makes the chart more accessible to non-technical viewers who might not recognise Tableau's default field name format.

### Why Three Bars Are Nearly Equal — The Insight

The three Customer Segment bars are almost identical in length (Home Office 34.3%, Consumer 33.1%, Corporate 32.5%). In most dashboards, near-equal bars suggest "nothing interesting to see here." In this context, the near-equality is itself the business insight: **the business has achieved a balanced customer base with no dangerous over-dependence on any single segment.**

A pie chart would communicate this balance equally well (three near-equal slices are easily read), but the horizontal bar was preferred because:
1. It is consistent with the Category Profitability chart's design language
2. It allows direct comparison with the Category Profitability chart's bar lengths (which are very unequal) — the contrast reinforces that segment distribution is healthy while category distribution is not
3. The colour encoding (profit) is more naturally applied in a bar chart than a pie chart

### Customer Segment Filter

This sheet has its own Customer Segment filter panel (right side), allowing isolation of a single segment. The filter is also shared across other sheets via the workbook's shared view definition, enabling cross-sheet segment analysis.

---

## 6. Ship Mode Distribution — Horizontal Bar Chart

**Sheet name:** Ship Mode Distribution  
**Mark type:** Bar (Automatic)  
**Variables:** Ship Mode (y-axis, sorted descending by sales) × Sum of Sales (x-axis, custom title "Total Sales")  
**Colour encoding:** Sum of Profit  
**Filter:** Region dashboard action

### Why a Horizontal Bar Chart?

Ship mode is a discrete categorical variable with four values (Standard Class, Second Class, First Class, Same Day). A horizontal bar chart correctly encodes the sales magnitude as bar length and allows easy ranking comparison.

Horizontal rather than vertical orientation is used because:
1. Ship mode names are multi-word ("Standard Class", "Same Day") and read better as horizontal labels
2. The dashboard layout places this chart in the lower-right zone where horizontal bars fit naturally

### Why Sort by Sales Descending?

Sorting by sales descending (Standard Class first) immediately answers the question "which shipping mode handles the most volume?" The answer — Standard Class at approximately 56.5% of sales — is visible before reading any label because the first bar is longest.

### The Profit Colour Encoding Insight

The colour encoding on this chart reveals a strategically important pattern: premium shipping modes (Same Day, First Class) tend to have darker colour (higher profit per order). This is not because shipping speed itself generates profit, but because:
- Technology orders (highest margin) are more likely to use premium shipping
- Furniture orders (lowest margin) predominantly use Standard Class
- The shipping mode distribution therefore partially reflects the category mix

This correlation — visible only through the colour encoding — would be invisible in a simple bar chart showing only sales volume.

### Alternatives Considered and Rejected

| Alternative | Why Rejected |
|---|---|
| Pie chart | Four unequal slices (56.5%, 22.0%, 14.7%, 6.7%) would be readable in a pie, but the profit colour encoding is harder to apply in a pie than a bar |
| Stacked bar | Appropriate if showing delivery speed distribution within each ship mode; a potential enhancement for future versions |
| Scatter plot | Inappropriate for categorical ship mode vs continuous sales; no natural x-y relationship |

---

## 7. Dashboard Layout and Interaction Design

### 7.1 KPI Cards at the Top — Hierarchy of Information

The dashboard places four KPI cards in the upper row before any chart. This layout follows the **inverted pyramid** principle of business communication: the most important summary information (the four headline numbers) appears first; detail and context follow below.

A viewer who has only 10 seconds sees the four numbers and leaves with the essential story. A viewer who has 5 minutes explores the charts and leaves with strategic insight.

### 7.2 Sales Trend Below KPIs — Temporal Context

The Sales Trend chart spans the full width of the dashboard immediately below the KPI cards. This placement answers the follow-up question to the KPI numbers: "How did we get to these numbers, and in which direction are we heading?" Width-spanning placement reinforces that this is the most important chart — it gets the most horizontal real estate.

### 7.3 Regional Performance as Central Filter

The Regional Performance chart is positioned to enable the dashboard action. Its placement and visual weight signal to the user that clicking it does something — it is the interactive entry point to regional analysis.

### 7.4 Category Profitability and Segment Side by Side

Category Profitability and Customer Segment are placed in the lower section, allowing side-by-side comparison of two complementary questions: "What are we selling most profitably?" and "Who is buying?" Together they answer: "Are our most profitable categories being sold proportionally to all customer types?"

### 7.5 Colour Palette Consistency

All charts use the same sequential colour scale to encode profit. This consistency means the viewer only needs to learn the colour meaning once — darker = more profitable — and can apply that understanding across all four charts that use colour encoding.

---

## Summary Table

| Chart | Type | Mark | Dimension | Measure | 2nd Measure (Colour) | Primary Question |
|---|---|---|---|---|---|---|
| Total Sales | KPI Text | Text | — | SUM(Sales) | — | How much revenue? |
| Total Profit | KPI Text | Text | — | SUM(Profit) | — | How much profit? |
| Total Orders | KPI Text | Text | — | COUNTD(Order ID) | — | How many orders? |
| Average Rating | KPI Text | Text | — | AVG(Customer Rating) | — | Customer satisfaction? |
| Sales Trend View | Line | Line | Month | SUM(Sales) | — | Is revenue growing? |
| Regional Performance View | Vertical Bar | Bar | Region | SUM(Sales) | SUM(Profit) | Which region leads? |
| Category Profitability View | Horizontal Bar | Bar | Category | SUM(Profit) | SUM(Sales) | What earns most profit? |
| Customer Segment View | Horizontal Bar | Bar | Customer Segment | SUM(Sales) | SUM(Profit) | Who buys from us? |
| Ship Mode Distribution | Horizontal Bar | Bar | Ship Mode | SUM(Sales) | SUM(Profit) | How are orders shipped? |

---

*Chart Selection Justification based on Sales_Performance_Dashboard.twbx*  
*Business Analytics Assignment Part 4 | Student: Priya Singh | ID: 2511034*
