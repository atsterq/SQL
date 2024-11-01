# https://itresume.ru/

## Нумерация строк по дате 
easy

``` sql
SELECT o.ord_datetime::date dt, o.ord_datetime, o.ord_id, a.an_id ord_an,
ROW_NUMBER() OVER (partition by o.ord_datetime::date order by o.ord_datetime desc) as rn
FROM orders o JOIN analysis a on o.ord_an = a.an_id
ORDER BY dt asc, ord_datetime asc
```
## Рост продаж по сравнению с предыдущим днем
easy

``` sql
select *
from
(select date, value::int, lag(value::int, 1, 0::int) over (order by date) as lg
from (select date, sum(value) as value
from sales
group by date) t) tt
where value > lg
order by date

```
## Проранжировать баллы
easy

``` sql
SELECT score, DENSE_RANK() over (order by score desc) as rnk
from scores
order by score desc
```
