# **Assignment2**
-> creating new tables, columns and measures in PowerBI using **DAX**

## 1. New tables

- A new table named "updated orders table" is created using "__addcolumns__" fuction so that this new table contains all the columns of the existing "orders" table and 2 new created columns named "profit per unit" and "profit level".

the DAX expression is: 
 
    updated orders table = ADDCOLUMNS(Orders,"profit per unit",DIVIDE(Orders[Profit],Orders[Quantity],0),"profit level",IF(divide(Orders[Profit],Orders[Quantity],0)>8,"high profit","low profit"))

 - Another table named "sales table" is created using the "__selectcolumns__" fuction so that this new table consists of individual columns from the chosen "orders" table and one new mathematically created "profit percentage" column. 

 the DAX expression is:

      sales table = SELECTCOLUMNS(Orders,"product id",Orders[Product ID],"sales",Orders[Sales],"profit",Orders[Profit],"profit percentage",(DIVIDE(Orders[Profit],Orders[Sales],0)*100))
   
- Both the above mentioned functions are combined and used to create the third column "shipping summary table" where the individual columns from "orders" table are selected along with new mathematically created "total shipping cost" column from within the new table.

the DAX expression is:

    Shipping summary table = ADDCOLUMNS(SELECTCOLUMNS(Orders,"date of order",Orders[Order Date],"date of shipping",Orders[Ship Date],"region",Orders[Region],"shipping mode",Orders[Ship Mode],"shipping price",Orders[Shipping Cost],"total units",Orders[Quantity]),"total shipping cost",([shipping price]*[total units]))


## 2. New columns

- A new column named "product value" is added to the independant "sales table" to classify the products into high valued and low valued according to their sales value and profit percentage

the DAX expression is:

    product value = IF(AND('sales table'[sales]>100,'sales table'[profit percentage]>15),"high value","low value")

- Another column named "days to ship" is added to the "shiping summary table" using the function "**datediff**" to calculate the number of days between order date and shipping date

the DAX expression is:

    dates to ship = DATEDIFF('Shipping summary table'[date of order],'Shipping summary table'[date of shipping],DAY)

- 2 new columns to find the year of order and quarter of that year named "order year" and "order year quarter"  is added to the "shipping summary table" using the "**year**" and "**quarter**" functions respectively.

the DAX expression is:

    order_year = YEAR('Shipping summary table'[date of order])
    


    order_year_quarter = QUARTER('Shipping summary table'[date of order])

- A column for calculating the sum of sales yet to date is created in "sales" table named "salesYTD" using "**totalytd**" function.

the DAXexpression is:

    salesYTD = TOTALYTD(sum(Orders[Sales]),Orders[order date])

- Another column for finding the rounded value of profit margin is created named "rounded profit margin" by using "**round**" function

the DAX expression is:

    rounded profit margin = ROUND(DIVIDE(Orders[Profit],Orders[Sales],0),2)
## 3. New measure

- A new measure "total discount" is created to the "updated orders table" to calculate the sum of products of sales with its corresponding discount percentge. the function "**sumx**" is used here.

the DAX expression is:

    total discount = SUMX('updated orders table','updated orders table'[Sales]*'updated orders table'[Discount percentage])

- Another measure called "sales std_dev" is created to the "updated order table" to calculate the standard deviation of sales using "**stdev.p**" function.

the DAX expresson is:

    sales std_dev = STDEV.P(Orders[Sales])
