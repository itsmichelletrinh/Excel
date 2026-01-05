# The Candle Factory

## 📚 Table of Contents
- [Business Task](#business-task)
- [Assignment #1 Question and Solution](#assignment-1-question-and-solution)
- [Assignment #2 Question and Solution](#assignment-2-question-and-solution)
- [Assignment #3 Question and Solution](#assignment-3-question-and-solution)

Please note that all assignment data and questions are created by the University of Waterloo, School of Computer Science for the [CS100: Introduction to Computing through Applications](https://student.cs.uwaterloo.ca/~cs100/****) course. 

***

## Business Task
To evaluate students' ability to effectively use spreadsheets to process, manipulate, and visualize data, students were assigned to use the data to analyze the candle factory's sales for January 2022 across several locations in Ontario, Canada; the online sales of a list of customers to generate a personal order thank you message; and to summarize a spreadsheet of customer information for number of customers and amount spent per city, number of candles sold per candle scent, overall expenses and profit, and to visualize the results in a pivot chart and pie chart. 

***

## Assignment 1 Question and Solution

All cells were pre-populated and students were expected to fill in orange-coloured cells (`M3:M6`, `K10:N22`, `C24:N24`, `C25:J25`). 

For efficiency, 5 named cells/ranges were created as indicated by the green-coloured cells in `M26:N32`. These include `Candle_Counts` (`C24:J24`), `Cost_Per_Candle` (`C4`), `GST` (`C6`), `HST` (`C5`), and `Total_Sales` (`N10:N22`).

**1. What is the subtotal for each location?**

````excel
=(PRODUCT(SUM(C10:J10),Cost_Per_Candle))
````

#### Steps:
- Use **SUM** to add up all number of candles sold for Waterloo across `C10:J10` in `K10`.
- Use **PRODUCT** to multiply the sum previously calculated by `Cost_Per_Candle`.
- Drag formula to autofill down to `K22`.

***

**2. What is the PST for each location?**

````excel
=PRODUCT(K10,HST)
````

#### Steps:
- Use **PRODUCT** to multiply the subtotal for Waterloo calculated in `K10` by `HST` in `L10`.
- Drag formula to autofill down to `L22`.

***

**3. What is the GST for each location?**

````excel
=PRODUCT(K10,GST)
````

#### Steps:
- Use **PRODUCT** to multiply the subtotal for Waterloo calculated in `K10` by `GST` in `M10`.
- Drag formula to autofill down to `M22`.

***

**4. What is the total sales for each location?**

````excel
=SUM(K10:M10)
````

#### Steps:
- Use **SUM** to add up the subtotal, PST, and GST previously calculated between `K10:M10` in `N10`.
- Drag formula to autofill down to `N22`.

***

**5. What is the min sales overall?**

````excel
=MIN(Total_Sales)
````

#### Steps:
- Use **MIN** to determine smallest total sales value across the range defined by `Total_Sales`.

***

**6. What is the max sales overall?**

````excel
=MAX(Total_Sales)
````

#### Steps:
- Use **MAX** to determine largest total sales value across the range defined by `Total_Sales`.

***

**7. What is the average sales overall?**

````excel
=AVERAGE(Total_Sales)
````

#### Steps:
- Use **AVERAGE** to determine the average of all total sales values across the range defined by `Total_Sales`.

***

**8. What are the totals for each candle scent, subtotal, PST, GST, and total sales?**

````excel
=SUM(C10:C22)
````

#### Steps:
- Use **SUM** to add up the number of candles sold for Balsam Fir scent across all locations across the range `C10:C22` in `C24`.
- Drag formula to autofill across to `N24`.

***

**9. Rank the candle scents by number of candles sold.**

````excel
=RANK(C24,Candle_Counts,0)
````

#### Steps:
- Use **RANK** to rank the total number of candles sold for Balsam Fir in `C24` in `C25` against all other scents across the range defined by `Candle_Counts`, specifying the `[order]` parameter as `0` to rank in descending order.
- Drag formula to autofill across to `J25`.

***

## Assignment 2 Question and Solution

All cells were pre-populated and students were expected to fill in the following cells: `'Customer Information'!G9:L34`, `'Customer Information'!K36`, `'Candle Information'!D3:F10`, `'Candle Information'!D12:F12`. 

For efficiency, 5 named cells/ranges were created as indicated by the green-coloured cells in `'Customer Information'!B36:C42`. These include `Candle_Scent_Costs` (`'Candle Information'!B3:C10`), `Discount` (`'Customer Information'!C3`), `GST` (`'Customer Information'!C6`), `Minimum_order_for_Discount` (`'Customer Information'!C4`), and `PST` (`'Customer Information'!C5`).

***

**1. What is the subtotal for each order?**

````excel
=VLOOKUP(E9,Candle_Scent_Costs,2,FALSE)*F9
````

#### Steps:
- In the `Customer Information` sheet:
- Use **VLOOKUP** in `G9` to retrieve price of the candle scent ordered by Axel Allen, where `E9` specifies the candle scent `lookup_value` parameter, `Candle_Scent_Costs` is the `table_array` parameter, `2` refers to the `col_index_num` parameter, and `FALSE` to find an exact match.
- Multiply the VLOOKUP value by the number of candles ordered in `F9`.
- Drag formula to autofill down to `G34`.

***

**2. What is the discount for each order?**

````excel
=IF(F9>=Minimum_order_for_Discount,G9*Discount,0)
````

#### Steps:
- In the `Customer Information` sheet:
- Use **IF** in `H9` to create a logical test where in the case that the number of candles ordered (`F9`) is >= `Minimum_order_for_Discount`, then calculate the discount as the subtotal (`G9`) multipled by the discount percentage (`Discount`). Otherwise, if the statement is not true, return `0`.
- Drag formula to autofill down to `H34`.

***

**3. What is the PST for each order?**

````excel
=G9*PST
````

#### Steps:
- In the `Customer Information` sheet:
- Multiply the subtotal in `G9` by `PST` in `I9`.
- Drag formula to autofill down to `I34`.

***

**4. What is the GST for each order?**

````excel
=G9*GST
````

#### Steps:
- In the `Customer Information` sheet:
- Multiply the subtotal in `G9` by `GST` in `J9`.
- Drag formula to autofill down to `J34`.

***

**5. What is the total for each order?**

````excel
=SUM(G9,I9,J9,-H9)
````

#### Steps:
- In the `Customer Information` sheet:
- Use **SUM** in `K9` to add up the subtotal in `G9`, discount in `H9`, PST in `I9`, and GST in `J9`. A `-` is placed in front of the `H9` discount value to subtract the discount amount. 
- Drag formula to autofill down to `K34`.

***

**6. Write a personal message for each order with the following format: Thank you [first name] [last name] for purchasing [candle scent] candles from The Candle Factory! (If there was a discount: You saved $[discount]!)**

````excel
=CONCATENATE("Thank you ",D9," ",C9," for purchasing ",E9," candles from The Candle Factory! ",IF(H9>0,CONCATENATE("You saved $",H9,"!"),""))
````

#### Steps:
- In the `Customer Information` sheet:
- Use **CONCATENATE** in `L9` to form the message with static and dynamic parameters.
- Use **IF** to create a logical test in the final parameter where in the case that there is a discount (`H9>0`), use CONCATENATE to add the discount sentence to the message. Otherwise, if the statement is not true, return a blank space (`""`). 
- Drag formula to autofill down to `L34`.

***

**7. What is the grand total of all orders?**

````excel
=SUM(K9:K34)
````

#### Steps:
- In the `Customer Information` sheet:
- Use **SUM** to add up the totals from all orders in the range of `K9:K34` in `K36`.

***

**8. What is the number of orders for each candle scent?**

````excel
=COUNTIF('Customer Information'!$E$9:$E$34,'Candle Information'!B3)
````

#### Steps:
- In the `Candle Information` sheet:
- Use **COUNTIF** in `'Candle Information'!D3` to create a conditional statement to count the number of orders in the range of `'Customer Information'!$E$9:$E$34` in the case that the candle scent ordered is equal to `'Candle Information'!B3`. The range uses `$` to create an absolute reference to ensure the same range is used when the formula is copied down.
- Drag formula to autofill down to `'Candle Information'!D10`.

***

**9. What is the total number of candles sold for each candle scent?**

````excel
=SUMIF('Customer Information'!$E$9:$E$34,'Candle Information'!B3,'Customer Information'!$F$9:$F$34)
````

#### Steps:
- In the `Candle Information` sheet:
- Use **SUMIF** in `'Candle Information'!E3` to create a conditional statement to add up the number of candles sold in the range of `'Customer Information'!$F$9:$F$34` in the case that the candle scent ordered (`'Customer Information'!$E$9:$E$34`) is equal to `'Candle Information'!B3`. Absolute references are created for the ranges to ensure the same range is used when the formula is copied down.
- Drag formula to autofill down to `'Candle Information'!E10`.

***

**10. What is the total number of orders with discounted candles for each candle scent?**

````excel
=COUNTIFS('Customer Information'!$E$9:$E$34,'Candle Information'!B3,'Customer Information'!$H$9:$H$34,">0")
````

#### Steps:
- In the `Candle Information` sheet:
- Use **COUNTIFS** in `'Candle Information'!F3` to create a conditional statement to count the number of orders in the case that the candle scent ordered (`'Customer Information'!$E$9:$E$34`) is equal to `'Candle Information'!B3` and there is a discount (`'Customer Information'!$H$9:$H$34,">0"`). Absolute references are created for the ranges to ensure the same range is used when the formula is copied down.
- Drag formula to autofill down to `'Candle Information'!F10`.

***

**11. What is the total number of orders across all candle scents?**

````excel
=SUM(D3:D10)
````

#### Steps:
- In the `Candle Information` sheet:
- Use **SUM** to add up the number of orders from all candle scents in the range of `D3:D10` in `D12`.

***

**12. What is the total number of candles sold across all candle scents?**

````excel
=SUM(E3:E10)
````

#### Steps:
- In the `Candle Information` sheet:
- Use **SUM** to add up the total number of candles sold from all candle scents in the range of `E3:E10` in `E12`.

***

**13. What is the total number of orders with discounted candles across all candle scents?**

````excel
=SUM(F3:F10)
````

#### Steps:
- In the `Candle Information` sheet:
- Use **SUM** to add up the total number of orders with discounted candles from all candle scents in the range of `F3:F10` in `F12`.

***

## Assignment 3 Question and Solution

All cells were pre-populated and students were expected to fill in the blue-coloured cells (`'Customer Information'!H:M`, `'Summary'!C3:D16`, `'Summary'!C20:C22`, `'Summary'!C25`, `'Summary'!H3:10`). 

For efficiency, 10 named cells/ranges were created. These include `Candle_IDs` (`'Products'!B4:C11`), `Candle_Info` (`'Products'!B4:D11`), `Candle_Prices` (`'Products'!C4:D11`), `Cities_Shipped_To` (`'Customer Information'!E2:E1001`), `Elsewhere_Shipping` (`'Products'!G4`), `GST` (`'Products'!G6`), `KW_Shipping` (`'Products'!G3`), `PST` (`'Products'!G5`), `Shipping` (`'Customer Information'!J2:J1001`), and `Totals` (`'Customer Information'!M2:M1001`). 

***

**1. What is the product name for each order?**

````excel
=VLOOKUP(G16,Candle_Info,2,FALSE)
````

#### Steps:
- In the `Customer Information` sheet:
- Use **VLOOKUP** in `H16` to retrieve the product name by matching product IDs, where `G16` specifies the associated product id `lookup_value` parameter, `Candle_Info` is the `table_array` parameter, `2` refers to the `col_index_num` parameter, and `FALSE` to find an exact match.
- Drag formula to autofill down `column H`.

***

**2. What is the subtotal for each order?**

````excel
=VLOOKUP(G16,Candle_Info,3,FALSE)*F16
````

#### Steps:
- In the `Customer Information` sheet:
- Use **VLOOKUP** in `I16` to retrieve the candle price by matching product IDs, where `G16` specifies the associated product id `lookup_value` parameter, `Candle_Info` is the `table_array` parameter, `3` refers to the `col_index_num` parameter, and `FALSE` to find an exact match.
- Multiply the VLOOKUP value by the number of candles purchased in `F16`.
- Drag formula to autofill down `column I`.

***

**3. What is the shipping cost for each order?**

````excel
=IF(OR(E16="Kitchener",E16="Waterloo"),I16*KW_Shipping,I16*Elsewhere_Shipping)
````

#### Steps:
- In the `Customer Information` sheet:
- Use **IF** in `J16` to create a logical test where in the case that the shipping location (`E6`) is `Kitchener` or `Waterloo` (`OR(E16="Kitchener",E16="Waterloo")`), multiply the subtotal (`I16`) by `KW_Shipping`. Otherwise, if the statement is not true, multiply the subtotal by `Elsewhere_Shipping`.
- Drag formula to autofill down `column J`.

***

**4. What is the PST for each order?**

````excel
=I16*PST
````

#### Steps:
- In the `Customer Information` sheet:
- Multiply the subtotal (`I16`) by `PST` in `K16`.
- Drag formula to autofill down `column K`.

***

**5. What is the GST for each order?**

````excel
=I16*GST
````

#### Steps:
- In the `Customer Information` sheet:
- Multiply the subtotal (`I16`) by `GST` in `L16`.
- Drag formula to autofill down `column L`.

***

**6. What is the total for each order?**

````excel
=SUM(I16:L16)
````

#### Steps:
- In the `Customer Information` sheet:
- Use **SUM** to add up the subtotal, shipping, PST, and GST found in the range of `I16:L16` in `M16`.
- Drag formula to autofill down `column M`.

***

**7. What is the total number of customers for each city?**

````excel
=COUNTIF(Cities_Shipped_To,Summary!B3)
````

#### Steps:
- In the `Summary` sheet:
- Use **COUNTIF** in `'C3` to create a conditional statement to count the number of customers in the range of `Cities_Shipped_To` in the case that the city is equal to `B3`.
- Drag formula to autofill down to `C15`.

***

**8. What is the total amount spent for each city?**

````excel
=SUMIF(Cities_Shipped_To,B3,Totals)
````

#### Steps:
- In the `Summary` sheet:
- Use **SUMIF** in `D3` to create a conditional statement to add up the order totals in the range of `Totals` in the case that the city (`Cities_Shipped_To`) is equal to `B3`.
- Drag formula to autofill down to `D15`.

***

**9. What is the total number of customers across all cities?**

````excel
=SUM(C3:C15)
````

#### Steps:
- In the `Summary` sheet:
- Use **SUM** in `C16` to add all the number of customers across all cities in the range of `C3:C15`.

***

**10. What is the total amount spent across all cities?**

````excel
=SUM(D3:D15)
````

#### Steps:
- In the `Summary` sheet:
- Use **SUM** in `D16` to add all the amount spent across all cities in the range of `D3:D15`.

***

**11. What is the total number of candles sold for each candle scent?**

````excel
=SUMIF('Customer Information'!$H$2:$H$1001,Summary!G3,'Customer Information'!$F$2:$F$1001)
````

#### Steps:
- In the `Summary` sheet:
- Use **SUMIF** in `H3` to create a conditional statement to add up the number of candles purchased in the range of `'Customer Information'!$F$2:$F$1001` in the case that the candle scent (`'Customer Information'!$H$2:$H$1001`) is equal to `G3`.
- Drag formula to autofill down to `H10`.

***

**12. What is the total shipping expense across all orders?**

````excel
=SUM(Shipping)
````

#### Steps:
- In the `Summary` sheet:
- Use **SUM** in `C20` to add all the shipping costs across all orders in the range of `Shipping`. 

***

**13. What is the total candle wax expense across all orders?**

````excel
=SUMPRODUCT(H3:H10,I3:I10)
````

#### Steps:
- In the `Summary` sheet:
- Use **SUMPRODUCT** in `C21` to first multiply all number of candles sold (`H3:H10`) by its assoicated wax cost (`I3:I10`), then sum the products.

***

**14. What is the overall profit?**

````excel
=D16-SUM(C20:C22)
````

#### Steps:
- In the `Summary` sheet:
- Use **SUM** to add the shipping, candle wax, and manufacturing expenses (`C20:C22`) to calculate total costs.
- Subtract the SUM value from total revenue (`D16`) to obtain profit. 

***
