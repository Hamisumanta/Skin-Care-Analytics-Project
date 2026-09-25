   CUSTOMER & RETENTION ANALYSIS

CUSTOMER KPI CARDS

Total Customers

Total Customers =

DISTINCTCOUNT(Sales[customer_id])

Repeat Customers

Repeat Customers =

COUNTROWS(  

FILTER(VALUES(Sales[customer_id]),
    
  CALCULATE(COUNTROWS(Sales)) > 1))

Repeat Customer Rate

Repeat Customer Rate =

DIVIDE( [Repeat Customers], [Total Customers], 0)

Revenue per Customer

Revenue per Customer =

DIVIDE([Total Revenue], [Total Customers], 0)

RFM_Base

RFM_Base =

VAR MaxDate =MAXX(ALL(Sales), Sales[created_at])

RETURN

ADDCOLUMNS(VALUES(Sales[customer_id]), "Recency_Days",

DATEDIFF(CALCULATE(MAX(Sales [created_at])), MaxDate, DAY),

"Frequency", CALCULATE(COUNTROWS(Sales)),
  
  "Monetary", CALCULATE(SUM(Transactions[gross_revenue_usd])))

RFM SCORE COLUMNS

Recency Score

R_Score =SWITCH(TRUE(),RFM_Base[Recency_Days] <= 90, 3, RFM_Base[Recency_Days] <= 180, 2,1)

Frequency Score

F_Score =SWITCH(TRUE(),
   
  RFM_Base[Frequency] >= 5, 3,
   
  RFM_Base[Frequency] >= 2, 2, 1)

Monetary Score

M_Score =SWITCH(TRUE(),

RFM_Base[Monetary] >= 200, 3,

RFM_Base[Monetary] >= 80, 2,1)

Total RFM Score

RFM_Total = RFM_Base[R_Score]+RFM_Base[F_Score]+RFM_Base[M_Score]
