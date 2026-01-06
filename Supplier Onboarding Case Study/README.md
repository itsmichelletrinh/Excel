# Supplier Onboarding Case Study

## 📚 Table of Contents
- [Business Task](#business-task)
- [Question #1 and Solution](#question-1-and-solution)
- [Question #2 and Solution](#question-2-and-solution)
- [Question #3 and Solution](#question-3-and-solution)

Please note that all case study data and questions are created by [Super.com](https://landing.super.com/about) to evaluate internship applicants.

***

## Business Task
As indicated in the `Instructions` sheet, applicants were provided with the following instructions:
````excel
At Super, we rely on suppliers to provide us with product inventory, which we sell to our customers.
Super is trying to decide which of the following suppliers to partner with first: Mercury, Venus, Mars, Earth.
We were able to obtain a list of the suppliers' products in their catalog in the 'Supplier Products' tab.
Additionally, we have the product demand insights for our customers on the 'Product Demand ' tab.

Keep in mind:
We want the most supply as possible, in high demand, across this Category priority:
````

| Our Priority | Category                   |
| ------------ | -------------------------- |
| 1            | Electronics                |
| 2            | Food, Beverages & Tobacco  |
| 3            | Toys & Games               |
| 4            | Apparel & Accessories      |
| 5            | Baby & Toddler             |

````excel
Using the data provided, please answer the questions listed below.
Please provide any excel, google sheet, or data points used in your analysis as well as a memo including the logic or methodology you used to develop your answers.
````

***

## Question 1 and Solution

**1. Who has the most "in demand" products?**

#### Steps:
- Created named ranges for efficiency, including:
  - `Supplier_Products` (`'Supplier Products'!A2:C987`) for a list of product `Title`, the associated `GTIN`, and the name of the `Supplier`.
  - `Supplier_Products_Supplier` (`'Supplier Products'!C2:C987`) to extract only the `Supplier` column.
  - `Supplier_Products_GTIN` (`'Supplier Products'!B2:B987`) to extract only the `GTIN` column.
  - `Relative_Demand` (`'Product Demand'!B2:B2021`) to extract only the `Relative Demand` column.
  - `Product_Demand_Supplier` (`'Product Demand'!J2:J2021`) to extract only the `Supplier` column.
  
- `Product Demand` sheet includes all products that are demanded by Super.com customers, so we need to determine who supplies these products. However, cannot match just `GTIN` or product `Title` with `Supplier`. There are   instances where products are missing `GTIN` or product `Title` so we need to match by both `GTIN` and `Title` to account for missing sets of information.
- Create `Supplier (Product Title)` column in `Product Demand` sheet and use **VLOOKUP** to search product `Title` (`C2`) in the `Supplier_Products` named range to retrieve `Supplier`.
- Drag formula to autofill down `Supplier (Product Title)` column.
 
````excel
=VLOOKUP(C2, Supplier_Products, 3,FALSE)
````

  - Create `Supplier (GTIN)` column in `Product Demand` sheet and use **INDEX** and **MATCH** to search `GTIN` (`D2`) in the `Supplier_Products_GTIN` named range and retrieve `Supplier` from `Supplier_Products_Supplier`.
  - Drag formula to autofill down `Supplier (GTIN)` column.
 
````excel
=INDEX(Supplier_Products_Supplier,MATCH('Product Demand'!D2, Supplier_Products_GTIN, 0))
````

  - Create `Supplier` column in `Product Demand` sheet and use **IFS** to create conditional statements to determine the finalized supplier for each product. With no matches from `Title` (`H2`)and `GTIN` (`I2`), return `No Supplier`. With matches from one of `Title` or `GTIN`, return `Supplier` from the option with no error. With matches from both `Title` and `GTIN`, return `Supplier` from the first option.

````excel
=IFS(AND(ISERROR(H2), ISERROR(I2)), "No Supplier",
     AND(ISERROR(H2), NOT(ISERROR(I2))), I2,
     AND(ISERROR(I2), NOT(ISERROR(H2))), H2,
     H2=I2, H2,
     NOT(H2=I2), I2)
````

- Use **COUNTIFS** to summarize results in `Analysis` sheet by counting how many products each supplier has in each `Relative Demand` category. Formula below shows an example for Earth's `Very High` product demand count.

````excel
=COUNTIFS(Relative_Demand, Analysis!B10, Product_Demand_Supplier, Analysis!$C$9)
````

- Create a custom scoring formula to determine a `Demand Sum` by summing the products of each supplier's demand counts (`C10, C11, C12, C13, C14`) and `Relative Demand` category. `Very High` demand provides the highest multiplier (`5`), while `Very Low` demand provides the lowest multiplier (`1`). Formula below shows an example for Earth.

````excel
=(C10*5)+(C11*4)+(C12*3)+(C13*2)+(C14*1)
````

- Use **RANK** to rank suppliers by their `Demand Sum` (`C16:F16`). Formula below shows an example of Earth's `Demand Rank`.

````excel
=RANK(C16, $C$16:$F$16,0)
````

#### Answer:

| Relative Demand | Earth | Mars | Mercury | Venus |
| --------------- | ----- | ---- | ------- | ----- |
| Very High       | 1     | 9    | 17      | 0     |
| High            | 15    | 141  | 34      | 0     |
| Medium          | 44    | 18   | 72      | 12    |
| Low             | 1     | 39   | 2       | 355   |
| Very Low        | 1     | 123  | 0       | 13    |
|                 |       |      |         |       |
| Demand Sum      | 200   | 864  | 441     | 759   |
| Demand Rank     | 4     | 1    | 3       | 2     |

- Mars has the most "in demand" products.

***

## Question 2 and Solution

**2. Who has the most products in our "targeted" categories?**

#### Steps:
- Created named ranges for efficiency, including:
  - `Ranking_Category_Path` (`'Product Demand'!G2:G2021`) to extract only the `Ranking Category Path` column.
  - `Product_Demand_Supplier` (`'Product Demand'!J2:J2021`) to extract only the `Supplier` column (from Q1).
 
- The `Product Demand` sheet built earlier in Q1 provides us with enough information to count the number of products each supplier has in each `Targeted Category`.
- Use **COUNTIFS** to summarize results in `Analysis` sheet by counting how many products each supplier has in each `Targeted Category`. Formula below shows an example for Earth's `Electronics` product count.

````excel
=COUNTIFS(Ranking_Category_Path, Analysis!B21, Product_Demand_Supplier, Analysis!$C$20)
````

- Create a custom scoring formula to determine a `Targeted Sum` by summing the products of each supplier's targeted category counts (`C21, C22, C23, C24, C25`) and `Targeted Category`. `Electronics` provides the highest multiplier (`5`), while `Baby & Toddler` provides the lowest multiplier (`1`). Formula below shows an example for Earth.

````excel
=(C21*5)+(C22*4)+(C23*3)+(C24*2)+(C25*1)
````

- Use **RANK** to rank suppliers by their `Targeted Sum` (`C27:F27`). Formula below shows an example of Earth's `Targeted Rank`.

````excel
=RANK(C27, $C$27:$F$27, 0)
````

#### Answer:

| Relative Demand | Earth | Mars | Mercury | Venus |
| --------------- | ----- | ---- | ------- | ----- |
| Very High       | 1     | 9    | 17      | 0     |
| High            | 15    | 141  | 34      | 0     |
| Medium          | 44    | 18   | 72      | 12    |
| Low             | 1     | 39   | 2       | 355   |
| Very Low        | 1     | 123  | 0       | 13    |
|                 |       |      |         |       |
| Demand Sum      | 200   | 864  | 441     | 759   |
| Demand Rank     | 4     | 1    | 3       | 2     |

- Mars has the most "in demand" products.
 
***
