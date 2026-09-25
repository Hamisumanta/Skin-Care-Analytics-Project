DAX MEASURES

Revenue

Revenue = SUM(Sales[Revenue])

Quantity Sold

Units = SUM(Sales[Quantity])

Profit

Profit = SUM(Sales[Profit])

Average Order Value

AOV = DIVIDE([Revenue],DISTINCTCOUNT(Sales[OrderID]))

Profit Margin

Profit Margin = DIVIDE([Profit],[Revenue])

Orders

Orders = DISTINCTCOUNT(Sales[OrderID])

Customers

Customers = DISTINCTCOUNT(Sales[CustomerID])

Discount %

Discount % = AVERAGE(Sales[Discount])
