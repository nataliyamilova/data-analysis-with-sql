##Свързване на таблици в SELECT

###Задача 4

Изведете коя куриерска фирма какви продукти е доставяла през 2015г 
( orders.ship_via = shippers.shipper_id )

| Company Name(Shippers) | Product Name | Quantity |
| ---                    | ----         | ---      |


```sql

	SELECT t1.company_name
, t4. product_name
, t3. quantity
, t2. order_date
FROM shippers t1
        INNER JOIN
     orders t2
        ON t2.ship_via = t1.shipper_id
        INNER JOIN
    order_details t3
        ON t3.order_id = t2.order_id
        INNER JOIN
    products t4
        ON t4.product_id = t3.product_id
         WHERE order_date BETWEEN '2015-01-01' AND '2015-12-31'	
		
```

###Задача 5

Кои служители са обслужвали клиентите с код ALFKI, BOLID, FISSA?


| Last Name | First Name | Company Name | Customer Code | Order Date |
| ---       | ---        | ---          | ---           | ---        |

```sql
SELECT t1.lastname
, t1.firstname
, t3.company_name
, t3.customer_code
, t2.order_date
FROM employees t1
        RIGHT OUTER JOIN
     orders t2
        ON t2.employee_id = t1.employee_id
        RIGHT OUTER JOIN
    customers t3
        ON t3.customer_id = t2.customer_id
WHERE t3.customer_code IN ('ALFKI', 'BOLID', 'FISSA')
ORDER BY 4
```

###Задача 6

Кои клиенти са закупували продукти от категориите SeaFood, Beverages?
( Total  e  unitprice * quantity )

| Category Name | CompanyName | OrderID | OrderDate | Product Name | Total |
| ---           | ---         | ---     | ---       | ---          | ---   |


```sql
SELECT t5. category_name
, t1. company_name
, t2. order_id
, t2. order_date
, t4. product_name
, t4. unit_price*quantity total
FROM customers t1
        LEFT OUTER JOIN
     orders t2
        ON t2.customer_id = t1.customer_id
        INNER JOIN
    order_details t3
        ON t3.order_id = t2.order_id
        INNER JOIN
    products t4
        ON t4.product_id = t3.product_id
        LEFT OUTER JOIN
    categories t5
        ON t5.category_id = t4.category_id
        WHERE t5.category_name IN ('Seafood', 'Beverages')
```

###Задача 7 

Изведете списък на служителите и продуктите, които те са продали през май 2015г.
В резултата трябва да присъства и кода на клиента. Колоната Total e unitprice *
quantity.

| Last Name | First Name | Product Name | Order Date | Customer Code | Total |
| ---       | ---        | ---          | ---        | ---           | ---   |

```sqlSELECT t1.lastname
, t1. firstname
, t4. product_name
, t2. order_date
, t5. customer_code
, t4. unit_price * quantity total
FROM employees t1
        LEFT OUTER JOIN
     orders t2
        ON t2.employee_id = t1.employee_id
        LEFT OUTER JOIN
    order_details t3
        ON t3.order_id = t2.order_id
        LEFT OUTER JOIN 
    products t4
        ON t4.product_id = t3.product_id
        RIGHT OUTER JOIN
    customers t5
        ON t5.customer_id = t2.customer_id
        WHERE order_date BETWEEN '2015-05-01' AND '2015-05-31'
        


```