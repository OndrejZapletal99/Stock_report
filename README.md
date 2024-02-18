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
      - [2.1.1 Parameter](#211-parameter)
---
## 1. Introduction
The purpose of this report is to create a complex overview of selected Stocks, ETFs, Crypto currencies.
The data source is [Yahoo Finance](https://finance.yahoo.com/).
## 2. Insert of the data
### 2.1 PowerQuery
#### 2.1.1 Parameter
1. First, It is necessary to create a new parameter in the powerquery to select different Stocks, ETFs, Crypto currencies.--> **"Stock Symbol"**

2. Second step is to insert data from yahoo online using the link--> https://query1.finance.yahoo.com/v8/finance/chart/

3. Third step is to clean all "Applied steps" on the right of the power query editor


4. Click through this source path to final destination with meta, timestamp and indicators
   - Record --> List --> Record 

5. Inserting new step "StartBranch" to "Applied steps"
6. Click on the "timestamp"
7. Convert to table via "To table" button