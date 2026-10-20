# ShopSmart Retail Sales Analysis

**Analyst:** ALU OLAMIDE  
**Project:** AnalystLab Africa — ShopSmart Analysis (Week 1)  
**Tools:** Microsoft Excel, PivotTables, charts, data modelling measures  
**Currency:** Nigerian naira (₦).

## Project overview

This project analyses ShopSmart's retail operations across sales, customers, 
products, stores, returns, suppliers, and inventory. The source contains a 
dashboard, calculation sheets, a data model, a cleaning log, business-question 
answers, and operational tables. This repository documents the analytical approach. 

## Business questions

- What are total revenue and quantity sold?
- Which products, categories, stores, months, customers, and regions lead sales?
- What is the return rate and which products/categories are returned most often?
- Which suppliers provide the most products?
- Which stores have SKUs below their reorder levels?
- Which product category is a candidate for further investment?

## Headline findings

| Metric |
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

## Key insights

**Beauty is the leading category** in the all-status analysis,
 with approximately ₦1.7625 billion in recorded line value (23.3% share) and 35,196 units.
 
**December is the strongest month** at approximately ₦660.6 million; 
February is the weakest at approximately ₦566.6 million.

**Store performance is tightly grouped.** STR015 Lagos leads the all-status 
ranking at approximately ₦311.9 million, but the leading store changes when
analysis is restricted to Completed orders.

**No single product dominates.** Home Item 400 (PROD0400) leads the all-status
product ranking at approximately ₦21.6 million, about 0.29% of recorded line value.

**Returns need monitoring.** The records 2,500 returns and ₦63.4 million
in refunds. Home and Beauty have the highest reported category return rates (about 5.2% each).

**Inventory replenishment:** 21 stocked SKUs are below their reorder level.
STR014 Port Harcourt and STR006 Kaduna each have three such SKUs; STR018 Ibadan has two.

**Supplier base is fragmented:** 489 suppliers are matched to 500 products
using the workbook's brand-to-supplier-name convention.

## Data model

This describes these entities:

- `Orders` — one product per order record, with date, quantity, price, discount, status, channel, and store/customer/product keys.
- `Customers` — customer profile and membership segment.
- `Products` — category, brand, cost and list selling price.
- `Stores` — store location and region.
- `Suppliers` — supplier master data.
- `Inventory` — stock on hand and reorder level by product/store.
- `Returns` — return reason and refund amount linked to orders.
- `Order_Items` — line-item table that mirrors `Orders` one-to-one.
- `Employees` — staff details by store.

Relationships:
- `Customers[Customer_ID]` 1 → * `Orders[Customer_ID]`
- `Products[Product_ID]` 1 → * `Orders[Product_ID]`
- `Stores[Store_ID]` 1 → * `Orders[Store_ID]`
- `Orders[Order_ID]` 1 → * `Returns[Order_ID]`
- `Products[Product_ID]` 1 → * `Inventory[Product_ID]`
- `Stores[Store_ID]` 1 → * `Inventory[Store_ID]`
- `Stores[Store_ID]` 1 → * `Employees[Store_ID]`

- # Methodology and limitations

## Workflow

a. Inspect source structure
-Identify the transaction fact table, dimension tables, keys, and field definitions.

b. Clean and validate 
-check duplicate rows, missing values, date types, numeric/currency
fields, key uniqueness, and foreign-key matches.

c. Calculate metrics
-use `Line_Total` as the recorded line value and aggregate quantity, orders,
returns, refunds, and inventory valuation.

d. Segment results
- compare by status, product, category, store, month, customer, region, and supplier.
e. Translate findings
-distinguish all-status order value from Completed-order value and connect findings to actions.

## Revenue definition

This states:

`Line_Total = Quantity × Unit_Price − Discount`

`Discount` is a flat amount (0–20) rather than a percentage. The 
recorded overall line value includes every order status. Therefore,
report the status basis next to each metric.

## Quality and interpretation cautions

A return *event count* is not necessarily the same as a count of
distinct orders returned. This reports 58 orders with two return 
records; retain these as separate return events unless a different
business rule is established. Customer email duplicates are reported 
for 49 customers. Do not assume this means duplicate customer records
without further review. Store names can repeat; use `Store_ID` as the store key.
Regions may not align to real-world geography. Product catalogue selling price
differs from order-level unit price. `Order_Items` mirrors `Orders` one-to-one.


## ANALYSIS
![DASHBOARD]<img width="584" height="549" alt="Untitled picture" src="https://github.com/user-attachments/assets/e639f1c9-cc4f-4595-aa34-03e6b36977a5" />

















![LINE CHART]<img width="1199" height="501" alt="Monthly sales trend ALA Project" src="https://github.com/user-attachments/assets/ce427682-d372-4d6f-aa6e-cb0cba8096cc" />



















![BARCHART]<img width="1181" height="510" alt="Revenue by Category ALA Poject" src="https://github.com/user-attachments/assets/20133cdf-68a8-4da2-bdc2-758b5f866aea" />




















![BARCHART]<img width="1213" height="516" alt="Revenue by State ALA Project" src="https://github.com/user-attachments/assets/08617251-30e9-432d-b756-048ab0f6402b" />




















![BARCHART]<img width="1209" height="513" alt="Sales by Region ALA Project" src="https://github.com/user-attachments/assets/ba5f30d8-7cd0-4e49-958a-e11a49c7097a" />



















![BARCHART]<img width="1208" height="500" alt="Sales by State ALA Project" src="https://github.com/user-attachments/assets/e8c8c20e-b565-42c2-b25a-38ad1181ef20" />





















# Findings and recommendations

## Sales quality

The sales totals ₦7.575 billion across 50,000 order records, 
but the amount includes Completed, Pending, and Cancelled statuses. 
Completed orders account for ₦2.497 billion; pending orders account
for ₦2.526 billion; cancelled orders account for ₦2.552 billion.

##Recommendation
Make order status visible on every sales dashboard. Use Completed 
orders for realised-sales reporting unless the business defines another 
recognised revenue policy. Label all-status metrics as recorded order value.

## Product and category performance

Beauty is the leading category by recorded line value at approximately
₦1.7625 billion (23.3%) and by units (35,196). The top product in the 
all-status ranking is Home Item 400 (PROD0400), with approximately ₦21.64 million.
The top product ranking changes for Completed orders.

##Recommendation
Maintain category-level visibility, validate profitability 
with cost data, and avoid making inventory decisions from revenue alone. Compare
Completed sales, gross margin, return rates, and stock availability together.

## Returns

There are 2,500 return records against 50,000 order records (5.0%)
and total refunds of approximately ₦63.44 million. Home and Beauty
have reported return rates around 5.2%.

##Recommendation
Review return reasons and product-level return rates, 
then investigate product descriptions, quality, fulfilment accuracy, and 
delivery performance. The workbook notes that some orders have multiple 
return records; count return events separately from distinct returned orders.

## Stores and regions

STR015 Lagos is the all-status store leader at approximately ₦311.9 million.

##Recommendation
Compare revenue per store, Completed revenue, order volume, 
returns, and inventory availability before reallocating resources. Treat 
regions as source labels rather than validated geographic groupings.

## Inventory and suppliers

Twenty-one of 500 stocked SKUs are below their reorder level. The supplier 
catalogue is highly fragmented: 489 suppliers for 500 products, with several
suppliers linked by deriving supplier names from brands.

##Recommendation
Prioritise below-reorder SKUs using sales velocity and lead time. Validate
supplier identity mapping before using it for procurement or supplier-risk decisions.

## Data quality checks recorded

The cleaning log reports:
- No fully duplicate rows removed across the listed datasets.
- No blank cells found in the inspected datasets.
- Zero mismatches between the summed `Orders.Line_Total` and `Order_Items.Line_Total`.
- Zero unmatched customer, product, store, return-order, or supplier lookups in its reconciliation checks.




