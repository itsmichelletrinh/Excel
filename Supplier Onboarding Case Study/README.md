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

  - Create `Supplier` column in `Product Demand` sheet and use **IFS** 

````excel
=IFS(AND(ISERROR(H2), ISERROR(I2)), "No Supplier", AND(ISERROR(H2), NOT(ISERROR(I2))), I2, AND(ISERROR(I2), NOT(ISERROR(H2))), H2, H2=I2, H2, NOT(H2=I2), I2)
````

***
