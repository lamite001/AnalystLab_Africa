# Methodology and limitations

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
differs from order-level unit price. `Order_Items` mirrors `Orders` one-to-one 
in this workbook, so aggregating both fact tables together can double-count sales.
Currency is assumed to be naira based on context; confirm with the data owner
before external reporting.


