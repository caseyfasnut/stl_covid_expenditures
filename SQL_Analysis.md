# SQL Analyses of St. Louis County COVID Expenditures (with Type)

## Spending on Various Items

The below query shows total amount and average dollar amount per purchase order for **Sanitizer**
```SQL
SELECT
    SUM(GROSS_AMOUNT) AS Total_Sanitizer_Exp,
    AVG(GROSS_AMOUNT) AS Avg_Sanitizer_Exp

FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE 
    COMMENT LIKE '%SANITIZER%'
    AND GROSS_AMOUNT  > 0
```
The Output: **Total_Sanitizer_Exp = $158,009.52**
            **Avg_Sanitizer_Exp = $1224.88**
