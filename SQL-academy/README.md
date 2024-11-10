# https://sql-academy.org/ru/trainer/tasks/17

## Задание 17
Определить, сколько потратил в 2005 году каждый из членов семьи. В результирующей выборке не выводите тех членов семьи, которые ничего не потратили.

``` sql
select f.member_name, f.status, sum(p.amount * unit_price) as costs
from FamilyMembers f join Payments p
on f.member_id = p.family_member
where YEAR(p.date) = '2005'
group by 1, 2
HAVING costs > 0
```
## Задание 18
Выведите имя самого старшего человека. Если таких несколько, то выведите их всех.
Поля в результирующей таблице:
member_name

``` sql
select member_name
from (
SELECT member_name, birthday, 
DATE_FORMAT(FROM_DAYS(DATEDIFF(NOW(),birthday)), '%Y') + 0 AS age,
max(DATE_FORMAT(FROM_DAYS(DATEDIFF(NOW(),birthday)), '%Y') + 0 ) over () as max_age
from FamilyMembers
) t
where age = max_age
```
## Задание 19

Определить, кто из членов семьи покупал картошку (potato)
Поля в результирующей таблице:
status
``` sql
select DISTINCT status
from FamilyMembers f
join Payments p on f.member_id = p.family_member
join Goods g on p.good = g.good_id
where good_name = 'potato'
```
## Задание 20

Сколько и кто из семьи потратил на развлечения (entertainment). Вывести статус в семье, имя, сумму
Поля в результирующей таблице:
``` sql
select f.status, f.member_name, 
sum(p.amount * p.unit_price) as costs
from FamilyMembers f
join Payments p on f.member_id = p.family_member
join Goods g on p.good = g.good_id
join GoodTypes gt on g.type = gt.good_type_id
where gt.good_type_name = 'entertainment'
group by 1, 2
```
## Задание 21

Определить товары, которые покупали более 1 раза
Поля в результирующей таблице:
good_name
``` sql
select  good_name
from Payments p join goods g
on p.good = g.good_id
group by good_name
having count(payment_id) > 1
```
## Задание 23

Найдите самый дорогой деликатес (delicacies) и выведите его цену
Поля в результирующей таблице:
good_name
unit_price
``` sql
select good_name, max(unit_price) as unit_price
from Payments p join Goods g on p.good = g.good_id
join GoodTypes gt on g.type = gt.good_type_id
where good_type_name = 'delicacies'
group by good_name
order by unit_price desc
limit 1
```
## 

``` sql

```
## 

``` sql

```## 

``` sql

```
## 

``` sql

```
## 

``` sql

```
## 

``` sql

```## 

``` sql

```
## 

``` sql

```
## 

``` sql

```
## 

``` sql

```## 

``` sql

```
## 

``` sql

```
## 

``` sql

```
## 

``` sql

```