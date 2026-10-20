# Methodology and limitations

## Workflow

1. **Inspect source structure
2. Identify the transaction fact table,
3. dimension tables, keys, and field definitions.
4. **Clean and validate:** check duplicate rows,
5.  missing values, date types, numeric/currency
6.  fields, key uniqueness, and foreign-key matches.
7. **Calculate metrics:** use `Line_Total` as the
8. recorded line value and aggregate quantity, orders,
9. returns, refunds, and inventory valuation.
10. **Segment results:** compare by status, product,
11.  category, store, month, customer, region, and supplier.
12. **Translate findings:** distinguish all-status order value
13. from Completed-order value and connect findings to actions.

## Revenue definition

This states:

`Line_Total = Quantity × Unit_Price − Discount`

`Discount` is a flat amount (0–20) rather than a percentage.
The recorded overall line value includes every order status. 
Therefore, report the status basis next to each metric.

## Quality and interpretation cautions

A return *event count* is not necessarily the same as a
count of distinct orders returned.
This reports 58 orders with two return records; retain
these as separate return events unless a different business
rule is established.
Customer email duplicates are reported for 49 customers.
Do not assume this means duplicate customer records without further review.
Store names can repeat; use `Store_ID` as the store key.
Regions may not align to real-world geography.
Product catalogue selling price differs from order-level unit price.
`Order_Items` mirrors `Orders` one-to-one in this workbook, so
aggregating both fact tables together can double-count sales.
Currency is assumed to be naira based on context; confirm with 
the data owner before external reporting.

## Reproducibility

The SQL and DAX files are starter examples. Adapt data types, table names, and status conventions to the target database/model, then reconcile calculated results with the source workbook.
