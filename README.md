# ShopSmart Retail Sales Analysis

**Analyst:** Alu Olamide  
**Project:** AnalystLab Africa — ShopSmart Analysis (Week 1)  
**Tools:** Microsoft Excel, PivotTables, charts, data modelling, SQL-ready analysis, Power BI-ready measures  
**Currency assumption:** Nigerian naira (₦), based on the Nigerian store/state context in the workbook.

## Project overview

This project analyses ShopSmart's retail operations across sales, customers, products, stores, returns, suppliers, and inventory. The source workbook contains a dashboard, calculation sheets, a data model, a cleaning log, business-question answers, and operational tables.

The repository documents the analytical approach and provides reusable SQL and DAX examples. The source workbook is **not included by default** because it contains customer contact fields. Review and anonymise data before publishing any source data publicly.

## Business questions

- What are total revenue and quantity sold?
- Which products, categories, stores, months, customers, and regions lead sales?
- What is the return rate and which products/categories are returned most often?
- Which suppliers provide the most products?
- Which stores have SKUs below their reorder levels?
- Which product category is a candidate for further investment?

## Headline findings from the workbook

| Metric | Workbook result |
|---|---:|
| Order records | 50,000 |
| Customers | 5,000 |
| Products | 500 |
| Stores | 25 |
| Suppliers | 489 |
| Recorded line revenue (all statuses) | ₦7,575,250,086 |
| Completed-order revenue | ₦2,496,824,383 |
| Pending-order value | ₦2,526,033,782 |
| Cancelled-order value | ₦2,552,391,921 |
| Revenue excluding cancelled orders | ₦5,022,858,165 |
| Units sold across all recorded statuses | 149,923 |
| Returns | 2,500 (5.0% of 50,000 order records) |
| Total refunds | ₦63,437,837 |
| Inventory value at cost | ₦3,169,020,818 |
| SKUs below reorder level | 21 of 500 |

> **Important interpretation note:** The workbook's headline total includes Completed, Pending, and Cancelled orders. It should be described as *recorded line value*, not realised revenue. For financial reporting, clearly define the status filter and use Completed orders where appropriate. Pending and cancelled amounts should not be treated as collected sales.

## Key insights

1. **Beauty is the leading category** in the workbook's all-status analysis, with approximately ₦1.7625 billion in recorded line value (23.3% share) and 35,196 units.
2. **December is the strongest month** at approximately ₦660.6 million; February is the weakest at approximately ₦566.6 million.
3. **Store performance is tightly grouped.** STR015 Lagos leads the all-status ranking at approximately ₦311.9 million, but the leading store changes when analysis is restricted to Completed orders.
4. **No single product dominates.** Home Item 400 (PROD0400) leads the all-status product ranking at approximately ₦21.6 million, about 0.29% of recorded line value.
5. **Returns need monitoring.** The workbook records 2,500 returns and ₦63.4 million in refunds. Home and Beauty have the highest reported category return rates (about 5.2% each).
6. **Inventory replenishment:** 21 stocked SKUs are below their reorder level. STR014 Port Harcourt and STR006 Kaduna each have three such SKUs; STR018 Ibadan has two.
7. **Supplier base is fragmented:** 489 suppliers are matched to 500 products using the workbook's brand-to-supplier-name convention.

## Data model

The workbook describes these entities:

- `Orders` — one product per order record, with date, quantity, price, discount, status, channel, and store/customer/product keys.
- `Customers` — customer profile and membership segment.
- `Products` — category, brand, cost and list selling price.
- `Stores` — store location and region.
- `Suppliers` — supplier master data.
- `Inventory` — stock on hand and reorder level by product/store.
- `Returns` — return reason and refund amount linked to orders.
- `Order_Items` — line-item table that mirrors `Orders` one-to-one in the supplied workbook.
- `Employees` — staff details by store.

Suggested relationships:
- `Customers[Customer_ID]` 1 → * `Orders[Customer_ID]`
- `Products[Product_ID]` 1 → * `Orders[Product_ID]`
- `Stores[Store_ID]` 1 → * `Orders[Store_ID]`
- `Orders[Order_ID]` 1 → * `Returns[Order_ID]`
- `Products[Product_ID]` 1 → * `Inventory[Product_ID]`
- `Stores[Store_ID]` 1 → * `Inventory[Store_ID]`
- `Stores[Store_ID]` 1 → * `Employees[Store_ID]`

Supplier matching in the workbook is based on `Brand` and a derived supplier name; validate this business rule before using it as a production key.

## Repository structure

```text
shopsmart-analysis-repo/
├── README.md
├── .gitignore
├── docs/
│   ├── data_dictionary.md
│   ├── methodology_and_limitations.md
│   └── findings.md
├── sql/
│   └── analysis_queries.sql
├── powerbi/
│   └── measures.dax
└── data/
    └── README.md
```

## How to use

1. Review the methodology and limitations in `docs/`.
2. Load the approved, cleaned datasets into your SQL environment or Power BI.
3. Adapt the table and column names in `sql/analysis_queries.sql` to your database.
4. Add the measures in `powerbi/measures.dax` after creating the corresponding model relationships.
5. Reconcile totals against the Excel workbook and confirm whether each report uses all statuses or Completed orders only.

## Data privacy

Do not publish customer names, email addresses, phone numbers, or other personal data in a public repository. Use synthetic/sample data or an approved anonymised extract. The original Excel workbook is intentionally excluded from this repository package.

## Limitations

- Currency is assumed to be Nigerian naira (₦); the workbook states that currency was not explicitly provided in the source files.
- Store region labels are used as supplied and may not reflect actual geography.
- The workbook says `Discount` is a flat amount, not a percentage, and calculates `Line_Total = Quantity × Unit_Price − Discount`.
- `Orders.Unit_Price` differs from `Products.Selling_Price`; revenue calculations use the order-level price.
- The provided `Order_Items` table mirrors `Orders` one-to-one; avoid double-counting by summing both tables.
- Product/store rankings can change when restricted to Completed orders.
