# DAX-in-Power-BI

Project Details: <a href="https://lakshitsharma99.github.io/powerbi.html">Maven Market</a>

In the Calendar table, add a column named "Weekend" - Equals "Y" for Saturdays or Sundays (otherwise "N")

* Weekend = IF(OR('Calendar'[Day Name]=="Saturday",'Calendar'[Day Name]=="Sunday"),"Y","N")

In the Calendar table, add a column named "End of Month" - Returns the last date of the current month for each row

* End of Month = ENDOFMONTH('Calendar'[date].[Date])

In the Customers table, add a column named "Current Age" - Calculates current customer ages using the "birthdate" column and the TODAY() function

* Current Age = DATEDIFF(Customers[birthdate],TODAY(),YEAR)

In the Customers table, add a column named "Priority" - Equals "High" for customers who own homes and have Golden membership cards (otherwise "Standard")

* Priority = IF(AND(Customers[homeowner]=="Y",Customers[member_card]=="Golden"),"High","Standard")

In the Customers table, add a column named "Short_Country" - Returns the first three characters of the customer country, and converts to all uppercase

* Short_Country = upper(LEFT(Customers[Country/Region],3))

In the Customers table, add a column named "House Number" - Extracts all characters/numbers before the first space in the "customer_address" column

* House Number = LEFT(Customers[customer_address], SEARCH(" ", Customers[customer_address]))

In the Products table, add a column named "Price_Tier" - Equals "High" if the retail price is >$3, "Mid" if the retail price is >$1, and "Low" otherwise

* Price_Tier = IF(Products[product_retail_price]>3, "High", IF(Products[product_retail_price]>1, "Mid", "Low"))

In the Stores table, add a column named "Years_Since_Remodel" - Calculates the number of years between the current date (TODAY()) and the last remodel date

* Years_Since_Remodel = DATEDIFF(Stores[last_remodel_date],TODAY(), YEAR)

Create a new measure named "Weekend Transactions" to calculate transactions on weekends

* Weekend Transactions = CALCULATE([Total Transactions], 'Calendar'[Weekend] = "Y")

Create new measures named "All Transactions" and "All Returns" to calculate grand total transactions and returns (regardless of filter context)

* All Transactions = CALCULATE([Total Transactions], ALL(Transactions_Data))

* All Return = CALCULATE([Total Returns], ALL(Return_Data))

Create a new measure to calculate "Total Revenue" based on transaction quantity and product retail price, and format as $

* Total Revenue = SUMX(Transactions_Data,Transactions_Data[quantity] * RELATED(Products[product_retail_price]))

Create a new measure to calculate "Total Cost" based on transaction quantity and product cost, and format as $

* Total Cost = SUMX(Transactions_Data, Transactions_Data[quantity] * RELATED(Products[product_cost]))

Create a new measure named "Total Profit" to calculate total revenue minus total cost, and format as $

* Total Profit = Transactions_Data[Total Revenue]-Transactions_Data[Total Cost]

Create a new measure to calculate "Profit Margin" by dividing total profit by total revenue calculate total revenue

* Profit Margin = DIVIDE(Transactions_Data[Total Profit],Transactions_Data[Total Revenue])

Create a new measure named "Unique Products" to calculate the number of unique product names in the Products table

* Unique Products = DISTINCTCOUNT(Products[product_name])
