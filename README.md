# **Assignment2**
-> creating new tables, columns and measures in PowerBI using **DAX**

## 1. New tables

- A new table named "updated orders table" is created using "__addcolumns__" fuction so that this new table contains all the columns of the existing "orders" table and 2 new created columns named "profit per unit" and "profit level".

the DAX expression is: 
 
    updated orders table = ADDCOLUMNS(Orders,"profit per unit",DIVIDE(Orders[Profit],Orders[Quantity],0),"profit level",IF(divide(Orders[Profit],Orders[Quantity],0)>8,"high profit","low profit"))

 - Another table named "sales table" is created using the "__selectcolumns__" fuction so that this new table consists of individual columns from the chosen "orders" table and one new mathematically created "profit percentage" column. 

 the DAX expression is:

      sales table = SELECTCOLUMNS(Orders,"product id",Orders[Product ID],"sales",Orders[Sales],"profit",Orders[Profit],"profit percentage",(DIVIDE(Orders[Profit],Orders[Sales],0)*100))
   
- Both the above mentiones functions are combined and used to create the third column "shipping summary table" where the individual columns from "orders" table are selected along with new mathematically created "total shipping cost" column from within the new table.

the DAX expression is:

    Shipping summary table = ADDCOLUMNS(SELECTCOLUMNS(Orders,"date of shipping",Orders[Ship Date],"region",Orders[Region],"shipping mode",Orders[Ship Mode],"shipping price",Orders[Shipping Cost],"total units",Orders[Quantity]),"total shipping cost",([shipping price]*[total units]))


## 2. New columns
