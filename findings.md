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

**Recommendation:** Maintain category-level visibility, validate profitability 
with cost data, and avoid making inventory decisions from revenue alone. Compare
Completed sales, gross margin, return rates, and stock availability together.

## Returns

There are 2,500 return records against 50,000 order records (5.0%)
and total refunds of approximately ₦63.44 million. Home and Beauty
have reported return rates around 5.2%.

**Recommendation:** Review return reasons and product-level return rates, 
then investigate product descriptions, quality, fulfilment accuracy, and 
delivery performance. The workbook notes that some orders have multiple 
return records; count return events separately from distinct returned orders.

## Stores and regions

STR015 Lagos is the all-status store leader at approximately ₦311.9 million.
The difference between the top and bottom store in the workbook's summary is 
relatively small. The South region leads total recorded value, but the workbook
notes that regional totals largely follow store counts.

##Recommendation Compare revenue per store, Completed revenue, order volume, 
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
- Date fields converted to true Excel dates and numeric/currency fields verified.

These are checks reported by the workbook, not an independent re-run of the source files.
