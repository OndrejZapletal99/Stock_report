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