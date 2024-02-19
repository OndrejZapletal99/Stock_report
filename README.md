# PowerBi report for Stock, ETf, Crypto history

- PowerBi:
  - PowerQuery
  - Dax
  - Visualisation

---

- ## Table of content
  - [1. Introduction](#1-introduction)
  - [2. Insert of the data](#2-insert-of-the-data)
    - [2.1. PowerQuery](#21-powerquerry)
    - [2.2 PowerBi date table](#22-powerbi-date-table)
    - [2.3 Measures](#23-measures)
---
## 1. Introduction
The purpose of this report is to create a complex overview of selected Stocks, ETFs, Crypto currencies.
The data source is [Yahoo Finance](https://finance.yahoo.com/).
## 2. Insert of the data
### 2.1 PowerQuery
1. First, It is necessary to create a new parameter in the powerquery to select different Stocks, ETFs, Crypto currencies.--> **"Stock Symbol"**

2. Second step is to insert data from yahoo online using the link--> https://query1.finance.yahoo.com/v8/finance/chart/

3. Third step is to clean all "Applied steps" on the right of the power query editor


4. Click through this source path to final destination with meta, timestamp and indicators
   - Record --> List --> Record 

5. Inserting new step "StartBranch" to "Applied steps"
6. Click on the "timestamp"
7. Convert to table via "To table" button
8. Transformation values into Date by custom column and formula
```
25569 + ([Column1]/60/60/24)
```
9. Change data type to Date
10. Insert index column
11. Rename last step to "EndBranchDate"
12. Insert new step after and rename it in the formula bar to StartBranch
13. Click on the "indicators"--> adjclose --> record --> List
14. Convert to table via "To table" button
15. 10. Insert index column and rename it into "EndBranchprice"
16. Merge querries together by iiner merge
17. Change "EndBranchprice" into "EndBranchDate" in the formula bar
18. Select "Date" from new column/table.
19. Remove index column
20. Rename "Stock Value" table into "Stock Value (new of your stock)
21. FOr others stocks etc only copy and paste of these two tables.
22. For all tables create new custom column "StockSymbol" and change datatype to text
23. Appanding all queries together by append queries

### 2.2 PowerBi date table
For every PowerBI report is better to create your own date table and after that connect the date table with others tables by relations.
1. Create a new table in PowerBI report.
```
Date table = CALENDAR(MINX(Appned_table,Appned_table[EndBranchprice.Date]), MAXX(Appned_table,Appned_table[EndBranchprice.Date]))
```
2. Create a new column for Year
```
Year = YEAR('Date table'[Date])
```
3. Create a new column for Month number
```
Month number = MONTH('Date table'[Date])
```
4. Create a new column for Month 
```
Month = FORMAT('Date table'[Month number],"MMM")
```
5. Create a new column for Day number
```
Day number = WEEKDAY(('Date table'[Date]),2)
```
6. Create a new column for Day 
- There is one problem if you have monday as a first day of the week. It is necessary to use switch expresion.
```
Day = 
SWITCH(
    WEEKDAY('Date table'[Date],2),
    1, "Monday",
    2, "Tuesday",
    3, "Wednesday",
    4, "Thursday",
    5, "Friday",
    6, "Saturday",
    7, "Sunday"
)
```
7. Create a new column for Quarter
```
Quarter = CONCATENATE("Q",QUARTER('Date table'[Date].[Date]))
```
8. Create a new column for Week number
```
Week number = WEEKNUM('Date table'[Date],2)
```
### 2.3 Measures
1. MIN
```
MIN = MINX(Appned_table,Appned_table[adjclose])
```
2. MAX
```
MAX = MAXX(Appned_table,Appned_table[adjclose])
```
3. Last Date
```
Last date = LASTDATE(Appned_table[EndBranchprice.Date])
```
4. Last date value
```
Last date  value = CALCULATE(
    [MAX],LASTDATE(Appned_table[EndBranchprice.Date]))
```
5. 52 Week max value
```
52 Week max value = CALCULATE(
    [MAX], DATESBETWEEN('Date table'[Date],TODAY()-365,TODAY()))
```
6. 52 Week min value
```
52 Week min value = CALCULATE(
    [MIN], DATESBETWEEN('Date table'[Date],TODAY()-365,TODAY()))
```
7. 52 Week max date
```
52 Week max date = LOOKUPVALUE(Appned_table[EndBranchprice.Date],Appned_table[adjclose],[52 Week max value])
```
8. 52 Week min date
```
52 Week min date = LOOKUPVALUE(Appned_table[EndBranchprice.Date],Appned_table[adjclose],[52 Week min value])
```
