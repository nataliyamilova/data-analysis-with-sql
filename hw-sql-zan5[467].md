## Изчисления в SELECT (Single-row Functions)
https://docs.oracle.com/cd/E11882_01/server.112/e41084/functions.htm#SQLRF006

### Задача 8 

Изведете списък на поръчките по години и месеци като резултата трябва да е 
сортиран по години и месеци в съответната година. Опитайте се да изведете 
месеца с името му.

| OrderID | Customer | Year  | Month  |
| ------- | -------- | ----- | ------ |
|         |          |       |        |

```sqlSELECT order_id
, customer_id
, EXTRACT (YEAR FROM order_date) YEAR
, EXTRACT (MONTH FROM order_date) MONTH
, to_char(order_date, 'Month' ) as MONTH
FROM orders
ORDER BY YEAR ASC

```
  
### Задача 9

Изведете списък с поръчките и дните, за които те са изпълнени. Като дните за 
изпълнение представляват разликата между order_date и shipped_date

| Order ID | Customer Code | Order Date | Days |
| -------- | ------------- | ---------- | ---- |
|          |               |            |      |

```sql
SELECT t1.order_id
,t2.customer_code
,t1.order_date
,TRUNC(t1.shipped_date - t1.order_date) Days
FROM orders t1
    INNER JOIN 
    customers t2
    ON
    t2.customer_id = t1.customer_id
```

### Задача 10

Изведете списък с клиентите като след името на фирмата следват държава и град 
(например: Астра ООД - България, София ), а лицата за контакт са само с фамилия 
и след фамилията следва телефон ( например: Иванов, 999-88-23 ).

| Customer Code | Company Name | Contact Name |
| ------------- | ------------ | ------------ |
|               |              |              |

```sql
SELECT customer_code
,company_name || ' - ' || country || ', ' || city || ' ' Company_name
, SUBSTR(contact_name,'',1)
|| SUBSTR(contact_name, INSTR(TRIM(contact_name), ' ', -1)) || ', ' || phone Contact_name

FROM customers

```

* същото с RegEx

```sql
```

### Задача 11  

Изведете списък с поръчките и продуктите закупени от клиента с код ALFKI като 
сумата платена за всеки продукт ( единична_цена х количество ) се представи 
в лева и USD ( в таблицата са в USD ) и е закръглена до втория знак.

| Customer Code | Order ID | Product Name | Total ( USD) | Total ( BGN ) |
| ------------- | -------- | ------------ | ------------ | ------------  |
|               |          |              |              |               |

```sql
SELECT t1.customer_code
, t2.order_id
, t4.product_name
, TO_CHAR(round(quantity * t4.unit_price, 2))  "Total (USD)"
, TO_CHAR(round(quantity * (t4.unit_price * 1.79), 2))  "Total (BGN)"
FROM customers t1
    INNER JOIN
    orders t2
    ON
    t2.customer_id = t1.customer_id
    INNER JOIN
    order_details t3
    ON
    t3.order_id = t2.order_id
    INNER JOIN
    products t4
    ON 
    t4.product_id = t3.product_id
    WHERE customer_code IN ('ALFKI')



```
