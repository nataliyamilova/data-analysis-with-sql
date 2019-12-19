## Агрегатни функции

### Задача 12 

В коя категория по колко продукта има?

| Category Name | Num Products |
| ------------- | ------------ |
|               |              |

```sql
SELECT t1.category_name
, t2.product_id
, COUNT(t2.quantity_per_unit) Numproducts
FROM categories t1
    INNER JOIN
    products t2
    ON
    t1.category_id = t2.category_id
    GROUP BY t1.category_name, t2.product_id;

```

### Задача 13 

Кой продукт в какво количество и на каква обща стойност е бил закупуван?

| Product Name | Total Quantity (units) | Total Sales ($) |
| ------------ | ---------------------- | --------------- |
|              |                        |                 |

```sql
SELECT t3.product_name
,  count(t2.quantity)total_unit
, TO_CHAR(SUM(t2.quantity*t2.unit_price),'$99,999.99') Total_quantity_
FROM orders t1
    INNER JOIN
    order_details t2
    ON t2.order_id = t1.order_id
    INNER JOIN
    products t3
    ON t3.product_id = t2.product_id
    GROUP BY
    t3.product_name





```

| Продукт | Кол-во  | Ед.цена |
| ------- | ------  | ------  |
| Ябълки  | 5       | 2       |
| Ябълки  | 2       | 2.5     |

| ------- | ------- | ------ |
| Ябълки  | 7       | 15     |


### Задача 14 

Kой служител на каква стойност поръчки е обслужвал през  периода 2014-2016г?
Данните трябва да са подредени по фамилия и година.

| Last Name | Year  | Total Sales ($) |
| --------- | ----- | --------------- |
|           |       |                 |

Получавам грешка в задачата, но не мога да открия каква е причината.
SELECT t1.lastname
, t2.order_date
, SUM(t3.quantity*t3.unit_price), Total

FROM employees t1
    INNER JOIN
    orders t2
    ON t2.employee_id = t1.employee_id
    INNER JOIN
    order_details t3
    ON t3.order_id = t2.order_id
    GROUP BY 
    t1.lastname
    t2.order_date
   





### Задача 15 

Направете отчет за всяка куриерска фирма по колко продукта  и поръчки е доставила
и каква стойността на поръчките.

| Company Name | Num Products | Num Orders  | Total Orders ($) |
| ------------ | ------------ | ----------- | ---------------- |
|              |              |             |                  |

```sql
```

### Задача 16

За всяка куриерска фирма да се направи отчет съдържащ:

| Company Name | MinProds | AvgProds | MAXProds | MinOrders | AvgOrders | MaxOrders |
| ------------ | -------- | -------  | -------- | --------  | --------- | --------  |
|              |          |          |          |           |           |           |


където:

MinProds - минимално количество доставени продукти с 1 поръчка (брой)
AvgProds - средно по колко продукта доставя (брой)
MaxProds - максимално количество доставени продукти с 1 поръчка (брой)

MinOrders - минимална стойност на доставена поръчка (USD $)
AvgOrders - средна стойност на доставена поръчка (USD $)
MaxOrders - максимална стойност на доставена поръчка (USD $)

```sql
```

# Вложени заявки (WITH)

## Задача 17

Направете отчет за общата стойност на поръчките по държави и клиенти, за които
общата стойност на поръчките е над средната за държавата, от която е клиента.

| Country | Company Name | Total |
| ------  | ------------ | ----  |
|         |              |       |


```sql
```

| Country | Company | Orderid | Total |
| ------- | ------- | ------- | ----- |
| BG      | X       | 11      | 100   |
| BG      | X       | 12      | 100   |
| BG      | X       | 13      | 100   |
| BG      | Y       | 14      | 100   |


BG Average: 200

| Country | Company | Total  |
| ------- | ------- | ------ |
| BG      | X       | 300    |



