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

All cells were pre-populated and students were expected to fill in orange-coloured cells (`M3:M6`, `K10:N22`, `C24:N24`. `C25:J25`). For efficiency, 5 named cells/ranges were created as indicated by the green-coloured cells in `M26:N32`. These include `Candle_Counts` (`C24:J24`), `Cost_Per_Candle` (`C4`), `GST` (`C6`), `HST` (`C5`), and `Total_Sales` (`N10:N22`).

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
