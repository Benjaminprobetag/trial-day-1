<p align="center"><a href="https://additive.eu" target="_blank"><img src="https://raw.githubusercontent.com/additive-apps/trial-day/master/logo.png" width="400"></a></p>


# 02 SQL (PostgreSQL)

Given the following Database:

Host: `ec2-54-220-215-8.eu-west-1.compute.amazonaws.com`

Port: `5432`

User: `trial-day`

PW: `p603b779a25b633f683b230ccaa75cb01230460b84e8b14cd155cead03909bbab`

Database: `dbem6ff3g5orbe`

Schema: `trial`

With it's tables

- organizations
- products
- orders

# Queries

Write a query to:

- get the total amount (amount_to_pay) of all orders per organisation per year ordered by year descending

    #### Expected Result:
    | Organization | Year | Amount |
    | ------------ | ---- | ----- |
    | Testhotel Post | 2021 | 123 |
    | ... | ... | ... |
    
     SELECT Sum(orders.amount_to_pay),
       organizations.NAME as "Organization Name",
       Extract(year FROM orders.created_at) as "Year"
FROM   organizations,
       orders
WHERE  organizations.id = orders.organization_id
GROUP  BY organizations.NAME,
          Extract(year FROM orders.created_at)
ORDER BY 2, 3 desc; 
---

- Get all organizations with at least 70 orders in the current year
    #### Expected Result:
  
    | Organization | Count |
    | ------------ | ----- |
    | Testhotel Post | 123 |
    | ... | ... |
    
    
    SELECT   Count(orders.organization_id) AS "value",
         organizations.NAME
FROM     organizations,
         orders
WHERE    organizations.id = orders.organization_id
AND      Extract(year FROM orders.created_at) = 2021
GROUP BY organizations.NAME
HAVING   Count(orders.organization_id) > 70 ;
---

Add your queries to this document and create a pull request at the end to complete your work.

## Bonus


- Do some further analysis
- get the most sold product per organisation

  #### Expected Result:

  | Organization | Product Name | Count |
  | ------------ | ---- | ----- |
  | Testhotel Post | Übernachtungsgutschein Einzelzimmer | 123 |
  | ... | ... | ... |
---
