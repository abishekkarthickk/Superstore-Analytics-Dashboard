# 📊 DAX Measures – Superstore Analytics Dashboard

This document contains all the DAX measures used in the **Superstore Analytics Dashboard** project.  
They are grouped by business requirement for clarity.

---

## Metrics

**Sales**
```DAX
Sales = SUM(Orders[Sales])
```
📌 Purpose: Calculates total sales revenue.

**Profit**
```DAX
Profit = SUM(Orders[Profit])
```
📌 Purpose: Calculates overall profit.

**% of Returned Orders**
```DAX
% of Returned Orders = 
VAR _total_orders = DISTINCTCOUNT(Orders[Order ID])
VAR _returned_orders = DISTINCTCOUNT(Returns[Order ID])
VAR _perc = DIVIDE(_returned_orders, _total_orders)
RETURN _perc
```
📌 Purpose: Percentage of orders that were returned.

## Previous Year (PY) Metrics

**Sales PY**
```DAX
Sales PY = 
CALCULATE(
    [Sales],
    SAMEPERIODLASTYEAR('Date table'[Date])
)
```
📌 Purpose: Calculates total sales for the previous year.

**Profit PY**
```DAX
Profit PY = 
CALCULATE(
    [Profit],
    SAMEPERIODLASTYEAR('Date table'[Date])
)
```
📌 Purpose: Calculates total profit for the previous year.

**% of Returned Orders PY**
```DAX
% of Returned Orders PY = 
CALCULATE(
    [% of Returned Orders],
    SAMEPERIODLASTYEAR('Date table'[Date])
)
```
📌 Purpose: Percentage of returned orders in the previous year.

## vs Previous Year (PY) – Growth %

**vs PY Sales**
```DAX
vs PY Sales = 
DIVIDE([Sales] - [Sales PY], [Sales PY])
```
📌 Purpose: Growth percentage in Sales compared to previous year.

**vs PY Profit**
```DAX
vs PY Profit = 
DIVIDE([Profit] - [Profit PY], [Profit PY])
```
📌 Purpose: Growth percentage in Profit compared to previous year.

**vs PY % Returned Orders**
```DAX
vs PY % Returned Orders = 
[% of Returned Orders] - [% of Returned Orders PY]
```
📌 Purpose: Change in return percentage compared to previous year.


## Date Table

**Date Table**
```DAX
Date table = 
ADDCOLUMNS(
    CALENDAR(MIN(Orders[Order Date]), MAX(Orders[Order Date])),
    "Start of Month", EOMONTH([Date], -1) + 1
)
```
📌 Purpose: Creates a continuous date table with a calculated “Start of Month” column.

---