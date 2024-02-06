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
