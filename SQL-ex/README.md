# SQL-ex
## Краткая информация о базе данных "Компьютерная фирма"
Схема БД состоит из четырех таблиц:  
Product(maker, model, type)  
PC(code, model, speed, ram, hd, cd, price)  
Laptop(code, model, speed, ram, hd, price, screen)  
Printer(code, model, color, type, price)  
Таблица Product представляет производителя (maker), номер модели (model) и тип ('PC' - ПК, 'Laptop' - ПК-блокнот или 'Printer' - принтер). Предполагается, что номера моделей в таблице Product уникальны для всех производителей и типов продуктов.  
В таблице PC для каждого ПК, однозначно определяемого уникальным кодом – code, указаны модель – model (внешний ключ к таблице Product), скорость - speed (процессора в мегагерцах), объем памяти - ram (в мегабайтах), размер диска - hd (в гигабайтах), скорость считывающего устройства - cd (например, '4x') и цена - price (в долларах).  
Таблица Laptop аналогична таблице РС за исключением того, что вместо скорости CD содержит размер экрана -screen (в дюймах).  
В таблице Printer для каждой модели принтера указывается, является ли он цветным - color ('y', если цветной), тип принтера - type (лазерный – 'Laser', струйный – 'Jet' или матричный – 'Matrix') и цена - price.

## Задание: 1

``` sql
Select model, speed, hd
from PC
where price < 500
```
## Задание: 2

``` sql
Select distinct p.maker 
from Product p
where p.type = 'printer'

```
## Задание: 3 

``` sql
Select model, ram, screen
from Laptop
where price > 1000

```
## Задание: 4

``` sql
Select *
from Printer
where color = 'y'

```
## Задание: 5

``` sql
Select model, speed, hd
from PC
where cd in ('12x', '24x') and price < 600

```
## Задание: 6

``` sql
SELECT DISTINCT Product.maker, Laptop.speed
FROM Product join Laptop on Product.model = Laptop.model 
WHERE Laptop.hd >= 10 AND 
 type = 'laptop'

```
## Задание: 7 

``` sql
select p.model, price
from (select model, price from PC
union
select model, price from Laptop
union
select model, price from Printer) as t
join product p on p.model = t.model
where p.maker = 'B'

```
## Задание: 8
Найдите производителя, выпускающего ПК, но не ПК-блокноты.
``` sql
Select maker
from product
where type in ('PC')
except 
select maker
from product
where type in ('Laptop')

```
## Задание: 9 
Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker
``` sql
select distinct p.maker
from product p
join PC pc on p.model = pc.model
where pc.speed >= 450

```
## Задание: 10 
Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price
``` sql
SELECT DISTINCT model, price
FROM Printer
WHERE price = (SELECT MAX(price) 
 FROM Printer
 )

```
## Задание: 11 
Найдите среднюю скорость ПК.
``` sql
Select AVG(speed)
from PC
```
## Задание: 12 
Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.
``` sql
Select avg(speed)
from laptop
where price > 1000

```
## Задание: 13
Найдите среднюю скорость ПК, выпущенных производителем A.
``` sql
Select avg(pc.speed)
from pc
join product on pc.model = product.model 
where product.maker = 'A'

```
## Задание: 14 
Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.

``` sql
Select s.class, s.name, c.country
from ships s join classes c on s.class = c.class
where c.numGuns >= 10

```
## Задание: 15
Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD
``` sql
Select hd
from pc
group by hd
having count(model) >= 2

```
## Задание: 16
Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.
``` sql
Select distinct a.model, b.model, a.speed, a.ram
from pc a join pc b
on a.speed = b.speed and a.ram = b.ram and a.model > b.model

```
## Задание: 17
Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК.
Вывести: type, model, speed
``` sql
Select distinct p.type, l.model, l.speed
from laptop l join product p on l.model = p.model
where l.speed < any (select min(pc.speed)
from pc)

```
``` sql
Select distinct 'Laptop' as type, l.model, l.speed
from laptop l 
where l.speed < any (select min(pc.speed)
from pc)

```
## 

``` sql
Select distinct p.maker, pr.price
from product p join printer pr on p.model = pr.model
where pr.price in (select min(price) from printer where color = 'y')
and color = 'y'
```
## Задание: 19 
Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов.
Вывести: maker, средний размер экрана.
``` sql
Select p.maker, avg(l.screen) as avg_screen
from product p join laptop l on p.model = l.model
group by p.maker

```
## Задание: 20 
Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.
``` sql
Select maker, count(model)
from product
where type = 'PC' 
group by maker
having count(model) >= 3

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

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
## 

``` sql

```
v