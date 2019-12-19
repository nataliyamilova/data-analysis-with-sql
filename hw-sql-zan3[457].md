
###Задача 2.1 (RE)

Всички клиенти, на които лицето за контакт има фамилия завършваща на 
"son" (напр. Maria Anderson) или "ez" (напр. Fernando Gozalez).

+---------------+--------------+--------------+---------+
| Customer Code | Company Name | Contact Name | Country |
+---------------+--------------+--------------+---------+

```sql
SELECT customer_code
, company_name
, contact_name
, country

FROM customers
WHERE REGEXP_LIKE(Contact_name, 'son$|ez$')
```

###Задача 2.2 (RE)

Всички продукти, които се продават в бутилки (колоната е quantity_per_unit)
от 12 oz (унции).

+------------+--------------+-------------------+------------+
| Product ID | Product Name | Quantity Per Unit | Unit Price |
+------------+--------------+-------------------+------------+

```sql
SELECT product_id
, product_name
, quantity_per_unit
, unit_price

FROM products
WHERE REGEXP_LIKE(quantity_per_unit,  'tles$') and REGEXP_LIKE(quantity_per_unit,  ' 12')
```
