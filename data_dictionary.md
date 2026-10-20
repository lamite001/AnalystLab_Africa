# Data dictionary (table-level summary)

| Table | Grain | Primary key | Important fields |
|---|---|---|---|
| `Orders` | One product/order transaction per row in this workbook | `Order_ID` | `Customer_ID`, `Product_ID`, `Store_ID`, `Order_Date`, `Quantity`, `Unit_Price`, `Discount`, `Shipping_Cost`, `Sales_Channel`, `Order_Status`, `Line_Total` |
| `Customers` | One customer per row | `Customer_ID` | Name, gender, age, city, state, registration date, customer segment |
| `Products` | One product per row | `Product_ID` | Product name, category, sub-category, brand, cost price, selling price, supplier name |
| `Stores` | One store per row | `Store_ID` | Store name, city/state, region, opening date |
| `Suppliers` | One supplier per row | `Supplier_ID` | Supplier name, contact and country fields |
| `Inventory` | One product/store inventory record per row | `Inventory_ID` | `Product_ID`, `Store_ID`, `Stock_On_Hand`, `Reorder_Level`, `Cost_Price`, `Stock_Value` |
| `Returns` | One return event per row | `Return_ID` | `Order_ID`, `Return_Date`, `Return_Reason`, `Refund_Amount`, `Product_ID`, `Category` |
| `Order_Items` | One order line per row | `Order_Item_ID` | `Order_ID`, `Product_ID`, `Quantity`, `Unit_Price`, `Discount`, `Line_Total` |
| `Employees` | One employee per row | `Employee_ID` | `Store_ID`, role, hire date, monthly salary |
| `Data_Dictionary` | One metadata entry per field | Dataset + Column | Field descriptions and key roles |

