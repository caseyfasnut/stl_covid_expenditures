# SQL Analyses of St. Louis County COVID Expenditures (with Type)

### I downloaded this data from a public [dataset](https://rdx.stldata.org/dataset/covid-expenditures-type) hosted on the [STL Regional Data Exchange](https://rdx.stldata.org) website.  This is a great resource that aggregates free datasets relevant to the St. Louis, Missouri Region. 
#### Please note that this dataset includes all expenditures AND FORMAL COMMITMENTS (less payroll) related to St. Louis County's response to COVID-19.  I included commitments in most cases in the below aggregate functions.  

## Spending by Item

The following query returns total amount and average dollar amount per purchase order for **SANITIZER**
```SQL
SELECT
    SUM(GROSS_AMOUNT) AS Total_Sanitizer_Exp,
    AVG(GROSS_AMOUNT) AS Avg_Sanitizer_Exp

FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE 
    COMMENT LIKE '%SANITIZER%'
    AND GROSS_AMOUNT  > 0 AND 
    COMMENT NOT LIKE '%MASKS%' AND 
    COMMENT NOT LIKE '%FACE SHIELDS%' AND 
    COMMENT NOT LIKE '%WIPES%'
```
The Output: **Total_Sanitizer_Exp = $155,158.58** and **Avg_Sanitizer_Exp = $1,261.45**

The following query returns total amount and average dollar amount per purchase order for **MASKS**
```SQL
SELECT
    SUM(GROSS_AMOUNT) AS Total_Masks_Exp,
    AVG(GROSS_AMOUNT) AS Avg_Masks_Exp

FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE 
    COMMENT LIKE '%MASKS%'AND 
    GROSS_AMOUNT  > 0 AND 
    COMMENT NOT LIKE '%SANITIZER%' AND 
    COMMENT NOT LIKE '%FACE SHIELDS%' AND 
    COMMENT NOT LIKE '%WIPES%'
```
The Output: **Total_Masks_Exp = $8,209,943.70** and **Avg_Masks_Exp = $59,064.34**


The following query returns total amount and average dollar amount per purchase order for **FOOD**
```SQL
SELECT 
    SUM(GROSS_AMOUNT) AS Total_Food_Exp,
    AVG(GROSS_AMOUNT) AS Avg_Food_Exp
    
FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE
     OBJECT != 'SPECIAL PROGRAM FUNDING' AND 
     OBJECT != 'OTHER PERSONAL SERVICES' AND
     GROSS_AMOUNT > 0 AND 
     COMMENT LIKE '%FOOD%' OR
     COMMENT LIKE '%LUNCH%'
```
The Output: **Total_Food_Exp = $44,936.89** and **Avg_Food_Exp = $356.64**

The following query returns the total amount and average amount per purchase order for **GLOVES**

```SQL
SELECT 
    SUM(GROSS_AMOUNT) AS Total_Gloves_Exp,
    AVG(GROSS_AMOUNT) AS Avg_Gloves_Exp

FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE
     GROSS_AMOUNT > 0 AND 
     COMMENT LIKE '%GLOVES%' AND 
     COMMENT NOT LIKE '%SANITIZER%' AND 
     COMMENT NOT LIKE '%MASKS%' AND 
     COMMENT NOT LIKE '%FACE SHIELDS%' AND 
     COMMENT NOT LIKE '%WIPES%'
```
The Output: **Total_Gloves_Exp = $168,401.20** and **Avg_Gloves_Exp = $1,810.77**

The following query returns the total amount and average amount per purchase order for **PLEXIGLASS**
```SQL
SELECT 
    SUM(GROSS_AMOUNT) AS Total_Plexiglass_Exp,
    AVG(GROSS_AMOUNT) AS Avg_Plexiglass_Exp

FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE 
    COMMENT LIKE '%PLEXIGLASS%' AND 
    GROSS_AMOUNT > 0 
```
The Output: **Total_Plexiglass_Exp = $23,144.39** and **Avg_Plexiglass_Exp = $5,786.10**

The following query returns the total amount and average amount per purchase order for **THERMOMETERS**
```SQL
SELECT
    SUM(GROSS_AMOUNT) AS Total_Thermometer_Exp,
    AVG(GROSS_AMOUNT) AS Avg_Thermometer_Exp
    
FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE
     GROSS_AMOUNT > 0 AND 
     COMMENT LIKE '%THERMOMETERS%'
```
The Output: **Total_Thermometer_Exp = $55,726.65** and **Avg_Thermometer_Exp = $4,643.89**

## A Few Items I Found Interesting

The following query returns the total amount and average amount per purchase order for **WebEx Licenses**
```SQL
SELECT 
    SUM(GROSS_AMOUNT) AS Total_WebEx_Exp,
    AVG(GROSS_AMOUNT) AS Avg_WebEx_Exp
    
FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE
     GROSS_AMOUNT > 0 AND 
     COMMENT LIKE '%WEBEX%'
```
The Output: **Total_WebEx_Exp = $141,369.22** and **Avg_WebEx_Exp = $17,671.15**

The following query returns the total amount spent on **WARRANTIES** (One record for "Laptop Warranties")
```SQL
SELECT 
    SUM(GROSS_AMOUNT) AS Total_Warranty_Exp,

FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE
     GROSS_AMOUNT > 0 AND 
     COMMENT LIKE '%WARRANTY%' OR
     COMMENT LIKE '%WARRANTIES%'
```
The Output: **Total_Warranty_Exp = $13,304.71**

The following query returns the total amount and average amount per purchase order for **LAPTOPS and PRINTERS**
```SQL
SELECT 
    SUM(GROSS_AMOUNT) AS Total_Tech_Exp,
    AVG(GROSS_AMOUNT) AS Avg_Tech_Exp
    
FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE
     GROSS_AMOUNT > 0 AND 
     COMMENT LIKE '%LAPTOPS%' OR 
     COMMENT LIKE '%LAPTOP%' OR
     COMMENT LIKE '%PRINTER%' OR
     COMMENT LIKE '%PRINTER%'
```
The Output: **Total_Tech_Exp = $381,454.54** and **Avg_Tech_Exp = $6,692.18**

The following query returns the total amount and average amount per purchase order for **MASS CASUALTY RELATED ITEMS (Tables, Bins, etc)**
```SQL
SELECT 
    SUM(GROSS_AMOUNT) AS Total_MC_Exp,
    AVG(GROSS_AMOUNT) AS Avg_MC_Exp
    
FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE
     GROSS_AMOUNT > 0 AND 
     COMMENT LIKE '%MASS%'
```
The Output: **Total_MC_Exp = $1,442,720.16** and **Avg_MC_Exp = $131,156.38**

The following query returns the total amount and average amount per purchase order for **PRINTING (Mailers, Postcards, Labels, etc)**
```SQL
SELECT 
    SUM(GROSS_AMOUNT) AS Total_Print_Exp,
    AVG(GROSS_AMOUNT) AS Avg_Print_Exp
    
FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE
     GROSS_AMOUNT > 0 AND 
     COMMENT LIKE '%PRINTING%'
```
The Output: **Total_Print_Exp = $38.524.60** and **Avg_Print_Exp = $4,815.58**

The following query returns the total amount and average amount per purchase order for **MICROSOFT OFFICE 365**
```SQL
SELECT 
    SUM(GROSS_AMOUNT) AS OFFICE_365
    
FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE
     GROSS_AMOUNT > 0 AND 
     COMMENT LIKE '%OFFICE 365%' AND 
     TRANSACTION_DESCRIPT !='PO Entry'
```
The Output: (Only one record) **OFFICE_365 = $16,182.00**

The following query returns the total amount and average amount per purchase order for **Ziploc Bags** (One result labeled "ZIPLOC BAG FOR COVID MASK")
```SQL
SELECT 
    SUM(GROSS_AMOUNT) AS Total_Ziploc_Exp
    
FROM `cert-project-308602.covid_expednditures.covid_expenditures`

WHERE
     GROSS_AMOUNT > 0 AND 
     COMMENT LIKE '%ZIPLOC%' AND 
     TRANSACTION_DESCRIPT != 'PO Entry'
```
The Output: **Total_Ziploc_Exp = $18,614.69**
