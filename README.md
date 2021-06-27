# Задачки из sql ex ru

## Краткая информация о базе данных "Компьютерная фирма":
Схема БД состоит из четырех таблиц:
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Таблица Product представляет производителя (maker), номер модели (model) и тип ('PC' - ПК, 'Laptop' - ПК-блокнот или 'Printer' - принтер). Предполагается, что номера моделей в таблице Product уникальны для всех производителей и типов продуктов. В таблице PC для каждого ПК, однозначно определяемого уникальным кодом – code, указаны модель – model (внешний ключ к таблице Product), скорость - speed (процессора в мегагерцах), объем памяти - ram (в мегабайтах), размер диска - hd (в гигабайтах), скорость считывающего устройства - cd (например, '4x') и цена - price. Таблица Laptop аналогична таблице РС за исключением того, что вместо скорости CD содержит размер экрана -screen (в дюймах). В таблице Printer для каждой модели принтера указывается, является ли он цветным - color ('y', если цветной), тип принтера - type (лазерный – 'Laser', струйный – 'Jet' или матричный – 'Matrix') и цена - price.

## Краткая информация о базе данных "Корабли":
Рассматривается БД кораблей, участвовавших во второй мировой войне. Имеются следующие отношения:
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Корабли в «классах» построены по одному и тому же проекту, и классу присваивается либо имя первого корабля, построенного по данному проекту, либо названию класса дается имя проекта, которое не совпадает ни с одним из кораблей в БД. Корабль, давший название классу, называется головным.
Отношение Classes содержит имя класса, тип (bb для боевого (линейного) корабля или bc для боевого крейсера), страну, в которой построен корабль, число главных орудий, калибр орудий (диаметр ствола орудия в дюймах) и водоизмещение ( вес в тоннах). В отношении Ships записаны название корабля, имя его класса и год спуска на воду. В отношение Battles включены название и дата битвы, в которой участвовали корабли, а в отношении Outcomes – результат участия данного корабля в битве (потоплен-sunk, поврежден - damaged или невредим - OK).
Замечания. 1) В отношение Outcomes могут входить корабли, отсутствующие в отношении Ships. 2) Потопленный корабль в последующих битвах участия не принимает.

## Краткая информация о базе данных "Фирма вторсырья":
Фирма имеет несколько пунктов приема вторсырья. Каждый пункт получает деньги для их выдачи сдатчикам вторсырья. Сведения о получении денег на пунктах приема записываются в таблицу:
Income_o(point, date, inc)
Первичным ключом является (point, date). При этом в столбец date записывается только дата (без времени), т.е. прием денег (inc) на каждом пункте производится не чаще одного раза в день. Сведения о выдаче денег сдатчикам вторсырья записываются в таблицу:
Outcome_o(point, date, out)
В этой таблице также первичный ключ (point, date) гарантирует отчетность каждого пункта о выданных деньгах (out) не чаще одного раза в день.
В случае, когда приход и расход денег может фиксироваться несколько раз в день, используется другая схема с таблицами, имеющими первичный ключ code:
Income(code, point, date, inc)
Outcome(code, point, date, out)
Здесь также значения столбца date не содержат времени.


## Краткая информация о базе данных "Аэрофлот":
Схема БД состоит из четырех отношений:
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Таблица Company содержит идентификатор и название компании, осуществляющей перевозку пассажиров. Таблица Trip содержит информацию о рейсах: номер рейса, идентификатор компании, тип самолета, город отправления, город прибытия, время отправления и время прибытия. Таблица Passenger содержит идентификатор и имя пассажира. Таблица Pass_in_trip содержит информацию о полетах: номер рейса, дата вылета (день), идентификатор пассажира и место, на котором он сидел во время полета. При этом следует иметь в виду, что
- рейсы выполняются ежедневно, а длительность полета любого рейса менее суток; town_from <> town_to;
- время и дата учитывается относительно одного часового пояса;
- время отправления и прибытия указывается с точностью до минуты;
- среди пассажиров могут быть однофамильцы (одинаковые значения поля name, например, Bruce Willis);
- номер места в салоне – это число с буквой; число определяет номер ряда, буква (a – d) – место в ряду слева направо в алфавитном порядке;
- связи и ограничения показаны на схеме данных.

**********************************************************************************************

### Задание: 1
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd
#### Решение:
SELECT PC.model, PC.speed, PC.hd FROM PC WHERE PC.price < 500

### Задание: 2
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите производителей принтеров. Вывести: maker
#### Решение:
SELECT DISTINCT Product.maker AS 'Maker' FROM Product  WHERE Product.type='Printer'

### Задание: 3
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.
#### Решение:
SELECT model, ram, screen FROM Laptop WHERE price > 1000

### Задание: 4
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите все записи таблицы Printer для цветных принтеров.
#### Решение:
SELECT * FROM Printer WHERE color = 'y'

### Задание: 5
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.
#### Решение:
SELECT model, speed, hd FROM PC WHERE (cd = '12x' OR cd = '24x') AND price < 600

### Задание: 6
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.
#### Решение:
SELECT DISTINCT Product.maker AS 'Maker', Laptop.speed FROM Product JOIN Laptop ON Product.model = Laptop.model WHERE Laptop.hd >= 10

### Задание: 7
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).
#### Решение:
SELECT Product.model, PC.price FROM Product JOIN PC ON Product.model = PC.model WHERE Product.maker = 'B'
UNION
SELECT Product.model, Laptop.price FROM Product JOIN Laptop ON Product.model = Laptop.model WHERE Product.maker = 'B'
UNION
SELECT Product.model, Printer.price FROM Product JOIN Printer ON Product.model = Printer.model WHERE Product.maker = 'B'

### Задание: 8
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите производителя, выпускающего ПК, но не ПК-блокноты.
#### Решение:
SELECT Product.maker AS 'Maker' FROM Product WHERE Product.type = 'PC' 
EXCEPT
SELECT Product.maker AS 'Maker' FROM Product WHERE Product.type = 'Laptop'

### Задание: 9
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker
#### Решение:
SELECT DISTINCT Product.maker AS 'Maker' FROM Product JOIN PC ON Product.model = PC.model WHERE PC.speed >=450

### Задание: 10
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price
#### Решение:
SELECT Printer.model, Printer.price FROM Printer WHERE Printer.price = (SELECT MAX(Printer.price) FROM Printer)

### Задание: 11
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите среднюю скорость ПК.
#### Решение:
SELECT AVG(PC.speed) FROM PC

### Задание: 12
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.
#### Решение:
SELECT AVG(Laptop.speed) FROM Laptop WHERE Laptop.price > 1000

### Задание: 13
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите среднюю скорость ПК, выпущенных производителем A.
#### Решение:
SELECT AVG(PC.speed) FROM PC JOIN Product ON Product.model = PC.model WHERE Product.maker = 'A'

### Задание: 14
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.
#### Решение:
SELECT Ships.class, Ships.name, Classes.country FROM Ships JOIN Classes ON Classes.class = Ships.class WHERE Classes.numGuns >=10

### Задание: 15
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD
#### Решение:
SELECT hd FROM pc GROUP BY (hd) HAVING COUNT(model) >= 2

### Задание: 16
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.
#### Решение:
SELECT DISTINCT p1.model, p2.model, p1.speed, p1.ram
FROM pc p1, pc p2
WHERE p1.speed = p2.speed AND p1.ram = p2.ram AND p1.model > p2.model

### Задание: 17
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК.
Вывести: type, model, speed
#### Решение:
SELECT DISTINCT Product.type, Laptop.model, Laptop.speed FROM Laptop JOIN Product ON Product.model = Laptop.model WHERE Laptop.speed < (SELECT MIN(PC.speed) FROM PC)

### Задание: 18
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите производителей самых дешевых цветных принтеров. Вывести: maker, price
#### Решение:
SELECT DISTINCT Product.maker, Printer.price FROM Product, Printer WHERE Product.model=Printer.model AND Printer.color = 'y' AND Printer.price = (SELECT MIN(Printer.price) FROM Printer WHERE Printer.color = 'y')

### Задание: 19
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов.
Вывести: maker, средний размер экрана.
#### Решение:
SELECT Product.maker, AVG(Laptop.screen) FROM Product JOIN Laptop ON Product.model = Laptop.model GROUP BY Product.maker

### Задание: 20
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.
#### Решение:
SELECT maker, COUNT(model)
FROM product
WHERE type = 'pc'
GROUP BY product.maker
HAVING COUNT (DISTINCT model) >= 3

### Задание: 21
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите максимальную цену ПК, выпускаемых каждым производителем, у которого есть модели в таблице PC.
Вывести: maker, максимальная цена.
#### Решение:
SELECT DISTINCT Product.maker, MAX(PC.price) FROM Product, PC WHERE Product.model = PC.model GROUP BY Product.maker

### Задание: 22
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Для каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.
#### Решение:
SELECT PC.speed, AVG(PC.price) FROM PC WHERE PC.speed > 600 GROUP BY PC.speed

### Задание: 23
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите производителей, которые производили бы как ПК
со скоростью не менее 750 МГц, так и ПК-блокноты со скоростью не менее 750 МГц.
Вывести: Maker
#### Решение:
SELECT DISTINCT Product.maker FROM Product JOIN PC ON Product.model=PC.model
WHERE PC.speed>=750 AND Product.maker IN (SELECT maker FROM Product JOIN Laptop ON Product.model=Laptop.model WHERE Laptop.speed>=750)

### Задание: 24
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Перечислите номера моделей любых типов, имеющих самую высокую цену по всей имеющейся в базе данных продукции.
#### Решение:
WITH CTE1 AS (SELECT PC.model, PC.price FROM PC
 UNION
 SELECT Laptop.model, Laptop.price FROM Laptop
 UNION
 SELECT Printer.model, Printer.price FROM Printer),

CTE2 AS (SELECT PC.price FROM PC
  UNION
  SELECT Laptop.price FROM Laptop 
  UNION
  SELECT Printer.price FROM Printer)

SELECT CTE1.model FROM CTE1 WHERE CTE1.price = (SELECT MAX(CTE2.price) FROM CTE2)

### Задание: 25
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите производителей принтеров, которые производят ПК с наименьшим объемом RAM и с самым быстрым процессором среди всех ПК, имеющих наименьший объем RAM. Вывести: Maker
#### Решение:
SELECT DISTINCT Product.maker
FROM Product
WHERE Product.model IN (
SELECT PC.model
FROM PC
WHERE PC.ram = (SELECT MIN(PC.ram) FROM PC)
AND PC.speed = (SELECT MAX(PC.speed) FROM PC WHERE PC.ram = (SELECT MIN(PC.ram) FROM PC)))
AND maker IN (SELECT Product.maker FROM Product WHERE Product.type='printer')

### Задание: 26
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите среднюю цену ПК и ПК-блокнотов, выпущенных производителем A (латинская буква). Вывести: одна общая средняя цена.
#### Решение:
WITH CTE AS (SELECT price, 1 AS num FROM PC, Product
 WHERE PC.model=Product.model AND Product.maker='A'
UNION ALL
 SELECT laptop.price, 1 AS num FROM laptop, Product
 WHERE laptop.model=Product.model AND Product.maker='A')

SELECT sum(CTE.price)/sum(CTE.num) AS averg FROM CTE

### Задание: 27
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найдите средний размер диска ПК каждого из тех производителей, которые выпускают и принтеры. Вывести: maker, средний размер HD.
#### Решение:
SELECT Product.maker, AVG(PC.hd) AS 'avrg'
FROM PC, Product WHERE Product.model = PC.model
AND Product.maker IN (SELECT DISTINCT Product.maker FROM Product WHERE Product.type = 'printer') GROUP BY Product.maker

### Задание: 28
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Используя таблицу Product, определить количество производителей, выпускающих по одной модели.
#### Решение:
SELECT COUNT(qty_inner) AS 'qty' FROM (
SELECT COUNT(Product.maker) AS 'qty_inner', Product.maker FROM Product GROUP BY Product.maker) sel WHERE sel.qty_inner = 1

### Задание: 29
Краткая информация о базе данных "Фирма вторсырья":
Income_o(point, date, inc)
Outcome_o(point, date, out)
Income(code, point, date, inc)
Outcome(code, point, date, out)
В предположении, что приход и расход денег на каждом пункте приема фиксируется не чаще одного раза в день [т.е. первичный ключ (пункт, дата)], написать запрос с выходными данными (пункт, дата, приход, расход). Использовать таблицы Income_o и Outcome_o.
#### Решение:
SELECT Income_o.point, Income_o.date, Income_o.inc, Outcome_o.out
FROM Income_o LEFT JOIN Outcome_o ON Income_o.point = Outcome_o.point
AND Income_o.date = Outcome_o.date
UNION
SELECT Outcome_o.point, Outcome_o.date, Income_o.inc, Outcome_o.out
FROM Income_o RIGHT JOIN Outcome_o ON Income_o.point = Outcome_o.point
AND Income_o.date = Outcome_o.date

### Задание: 30
В предположении, что приход и расход денег на каждом пункте приема фиксируется произвольное число раз (первичным ключом в таблицах является столбец code), требуется получить таблицу, в которой каждому пункту за каждую дату выполнения операций будет соответствовать одна строка.
Вывод: point, date, суммарный расход пункта за день (out), суммарный приход пункта за день (inc). Отсутствующие значения считать неопределенными (NULL).
#### Решение:
WITH CTE AS (SELECT Income.point, Income.date, SUM(Income.inc) AS sum_inc, NULL AS sum_out FROM Income GROUP BY Income.point, Income.date
UNION
SELECT Outcome.point, Outcome.date, NULL AS sum_inc, SUM(Outcome.out) AS sum_out FROM Outcome GROUP BY Outcome.point, Outcome.date)

SELECT CTE.point, CTE.date, SUM(CTE.sum_out), SUM(CTE.sum_inc) FROM CTE
GROUP BY CTE.point, CTE.date ORDER BY CTE.point

### Задание: 31
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Для классов кораблей, калибр орудий которых не менее 16 дюймов, укажите класс и страну.
#### Решение:
SELECT Classes.class, Classes.country FROM Classes WHERE Classes.bore >= 16

### Задание: 32
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Одной из характеристик корабля является половина куба калибра его главных орудий (mw). С точностью до 2 десятичных знаков определите среднее значение mw для кораблей каждой страны, у которой есть корабли в базе данных.
#### Решение:
WITH CTE AS (SELECT Classes.country, Classes.class, Classes.bore, Ships.name FROM Classes LEFT JOIN Ships ON Classes.class=Ships.class
UNION ALL
SELECT DISTINCT Classes.country, Classes.class, Classes.bore, Outcomes.ship FROM Classes LEFT JOIN Outcomes ON Classes.class=Outcomes.ship
WHERE Outcomes.ship=Classes.class AND Outcomes.ship NOT IN (SELECT Ships.name FROM Ships))

SELECT CTE.country, CAST(AVG((POWER(CTE.bore,3)/2)) AS NUMERIC(6,2)) AS weight
FROM CTE WHERE CTE.name IS NOT NULL GROUP BY CTE.country

### Задание: 33
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Укажите корабли, потопленные в сражениях в Северной Атлантике (North Atlantic). Вывод: ship.
#### Решение:
SELECT Outcomes.ship FROM Outcomes LEFT JOIN Battles ON Outcomes.battle=Battles.name WHERE Outcomes.battle='North Atlantic' AND Outcomes.result='sunk'

### Задание: 34
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
По Вашингтонскому международному договору от начала 1922 г. запрещалось строить линейные корабли водоизмещением более 35 тыс.тонн. Укажите корабли, нарушившие этот договор (учитывать только корабли c известным годом спуска на воду). Вывести названия кораблей.
#### Решение:
SELECT Ships.name FROM Classes, Ships WHERE Ships.class = Classes.class AND Ships.launched >= 1922 AND Classes.displacement>35000 AND Classes.type='bb'

### Задание: 35
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
В таблице Product найти модели, которые состоят только из цифр или только из латинских букв (A-Z, без учета регистра).
Вывод: номер модели, тип модели.
#### Решение:
SELECT Product.model, Product.type FROM Product WHERE LOWER(Product.model) NOT LIKE '%[^a-z]%' OR Product.model NOT LIKE '%[^0-9]%'

### Задание: 36
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Перечислите названия головных кораблей, имеющихся в базе данных (учесть корабли в Outcomes).
#### Решение:
SELECT Outcomes.ship FROM Outcomes JOIN Classes ON Classes.class=Outcomes.ship
UNION
SELECT Ships.name FROM Ships JOIN Classes ON Classes.class=Ships.name

### Задание: 37
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите классы, в которые входит только один корабль из базы данных (учесть также корабли в Outcomes).
#### Решение:
WITH CTE AS (
SELECT Ships.class, Ships.name FROM Ships 
UNION 
SELECT Outcomes.ship, Outcomes.ship FROM Outcomes
)

SELECT Classes.class FROM Classes LEFT JOIN CTE ON CTE.class = Classes.class GROUP BY Classes.class HAVING COUNT(CTE.name) = 1

### Задание: 38
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите страны, имевшие когда-либо классы обычных боевых кораблей ('bb') и имевшие когда-либо классы крейсеров ('bc').
#### Решение:
SELECT Classes.country FROM Classes GROUP BY Classes.country HAVING COUNT(DISTINCT Classes.type) = 2

### Задание: 39
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите корабли, `сохранившиеся для будущих сражений`; т.е. выведенные из строя в одной битве (damaged), они участвовали в другой, произошедшей позже.
#### Решение:
WITH CTE AS (SELECT Outcomes.ship, Battles.name, Battles.date, Outcomes.result FROM Outcomes LEFT JOIN Battles ON Outcomes.battle = Battles.name)

SELECT DISTINCT a.ship FROM CTE AS a WHERE UPPER(a.ship) IN (SELECT UPPER(b.ship) FROM CTE AS b WHERE b.date < a.date AND b.result = 'damaged')

### Задание: 40
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найти производителей, которые выпускают более одной модели, при этом все выпускаемые производителем модели являются продуктами одного типа.
Вывести: maker, type
#### Решение:
SELECT Product.maker, MAX(Product.type) AS 'type' FROM Product GROUP BY Product.maker HAVING COUNT(Product.model) > 1 AND COUNT(DISTINCT Product.type) = 1

### Задание: 41
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Для каждого производителя, у которого присутствуют модели хотя бы в одной из таблиц PC, Laptop или Printer,
определить максимальную цену на его продукцию.
Вывод: имя производителя, если среди цен на продукцию данного производителя присутствует NULL, то выводить для этого производителя NULL,
иначе максимальную цену.
#### Решение:
WITH CTE AS (
SELECT PC.model, PC.price FROM PC
UNION
SELECT Laptop.model, Laptop.price FROM Laptop
UNION
SELECT Printer.model, Printer.price FROM Printer)
 
SELECT Product.maker, 
CASE WHEN COUNT(CTE.price) = COUNT(*) THEN MAX(CTE.price) END
FROM Product, CTE WHERE Product.model=CTE.model GROUP BY Product.maker

### Задание: 42
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите названия кораблей, потопленных в сражениях, и название сражения, в котором они были потоплены.
#### Решение:
SELECT Outcomes.ship, Outcomes.battle FROM Outcomes WHERE Outcomes.result='sunk'

### Задание: 43
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Укажите сражения, которые произошли в годы, не совпадающие ни с одним из годов спуска кораблей на воду.
#### Решение:
SELECT Battles.name FROM Battles WHERE YEAR(Battles.date) NOT IN (SELECT Ships.launched FROM Ships WHERE Ships.launched IS NOT NULL)

### Задание: 44
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите названия всех кораблей в базе данных, начинающихся с буквы R.
#### Решение:
SELECT Ships.name FROM Ships WHERE Ships.name LIKE 'R%'
UNION
SELECT Outcomes.ship FROM Outcomes WHERE Outcomes.ship LIKE 'R%'

### Задание: 45
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите названия всех кораблей в базе данных, состоящие из трех и более слов (например, King George V).
Считать, что слова в названиях разделяются единичными пробелами, и нет концевых пробелов.
#### Решение:
WITH CTE AS (
SELECT Ships.name FROM Ships 
UNION 
SELECT Outcomes.ship FROM Outcomes)

SELECT * FROM CTE WHERE CTE.name LIKE '% % %'

### Задание: 46
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Для каждого корабля, участвовавшего в сражении при Гвадалканале (Guadalcanal), вывести название, водоизмещение и число орудий.
#### Решение:
WITH CTE AS (
SELECT Ships.name AS ship, Classes.displacement, Classes.numGuns FROM Ships JOIN Classes ON Classes.class=Ships.class
UNION
SELECT Classes.class AS ship, Classes.displacement, Classes.numGuns FROM Classes)

SELECT Outcomes.ship, CTE.displacement, CTE.numGuns FROM CTE RIGHT JOIN Outcomes ON Outcomes.ship=CTE.ship WHERE Outcomes.battle = 'Guadalcanal'

### Задание: 47
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Определить страны, которые потеряли в сражениях все свои корабли.
#### Решение:
WITH B AS (/* names from Outcomes AND Ships */
SELECT Outcomes.ship AS name FROM Outcomes
UNION ALL
SELECT Ships.name FROM Ships),

D AS ( /* names and class with replaced nones from Outcomes AND Ships */
SELECT B.name, CASE WHEN Ships.class IS NULL THEN B.name ELSE Ships.class END AS class FROM Ships RIGHT JOIN B ON Ships.name = B.name),

T AS (/* names and classes among sunked */
SELECT name, class FROM D LEFT JOIN Outcomes ON D.name = Outcomes.ship WHERE result='sunk'),

FINAL AS ( /* sunked country is intersection of counted sunked ships and counted all ships ordered by country */
SELECT Classes.country, COUNT(T.name) AS cnum FROM Classes
JOIN T ON Classes.class = T.class GROUP BY Classes.country 
INTERSECT
SELECT Classes.country, COUNT(D.name) AS cnum FROM Classes 
JOIN D ON Classes.class = D.class GROUP BY Classes.country)

SELECT country FROM FINAL


### Задание: 48
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите классы кораблей, в которых хотя бы один корабль был потоплен в сражении.
#### Решение:
WITH CTE AS (SELECT Classes.class, Outcomes.result FROM Classes JOIN Ships ON Ships.class=Classes.class JOIN Outcomes ON Ships.name=Outcomes.ship
UNION
SELECT Classes.class, Outcomes.result FROM Classes JOIN Outcomes ON Classes.class=Outcomes.ship)

SELECT class FROM CTE WHERE CTE.result='sunk'

### Задание: 49
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите названия кораблей с орудиями калибра 16 дюймов (учесть корабли из таблицы Outcomes).
#### Решение:
WITH CTE AS (
SELECT Ships.name, Classes.bore FROM Ships JOIN Classes ON Ships.class=Classes.class
UNION
SELECT Classes.class, Classes.bore FROM Classes JOIN Outcomes ON Classes.class=Outcomes.ship)

SELECT CTE.name FROM CTE WHERE CTE.bore=16

### Задание: 50
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите сражения, в которых участвовали корабли класса Kongo из таблицы Ships.
#### Решение:
WITH CTE AS (
SELECT Ships.class, Outcomes.battle FROM Outcomes 
LEFT JOIN Ships ON Ships.name=Outcomes.ship
LEFT JOIN Classes ON Ships.class=Classes.class)

SELECT DISTINCT CTE.battle FROM CTE WHERE CTE.class='Kongo'

### Задание: 51
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Найдите названия кораблей, имеющих наибольшее число орудий среди всех имеющихся кораблей такого же водоизмещения (учесть корабли из таблицы Outcomes).
#### Решение:
WITH CTE AS (
SELECT Classes.displacement, Ships.name, Classes.numGuns FROM Ships JOIN Classes ON Ships.class=Classes.class
UNION
SELECT Classes.displacement, Outcomes.ship, Classes.numGuns FROM Outcomes JOIN Classes ON Outcomes.ship=Classes.class),

CTE2 AS (SELECT CTE.displacement, MAX(CTE.numGuns) mxng FROM CTE GROUP BY CTE.displacement),

CTE3 AS (SELECT CTE.name, CTE.displacement, CTE.numGuns FROM CTE, CTE2 WHERE CTE.displacement=CTE2.displacement AND CTE.numGuns=CTE2.mxng)

SELECT name FROM CTE3

### Задание: 52
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Определить названия всех кораблей из таблицы Ships, которые могут быть линейным японским кораблем,
имеющим число главных орудий не менее девяти, калибр орудий менее 19 дюймов и водоизмещение не более 65 тыс.тонн
#### Решение:
WITH CTE AS (
SELECT Ships.name, Classes.type, Classes.country, Classes.numGuns, Classes.bore, Classes.displacement FROM Ships JOIN Classes ON Ships.class=Classes.class
WHERE Classes.type='bb' 
AND Classes.country='Japan' 
AND (Classes.numGuns>=9 OR numguns is NULL)
AND (Classes.bore<19 OR bore is NULL)
AND (Classes.displacement<=65000 OR displacement is NULL)
)

SELECT name FROM CTE

### Задание: 53
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Определите среднее число орудий для классов линейных кораблей.
Получить результат с точностью до 2-х десятичных знаков.
#### Решение:
WITH CTE AS (SELECT Classes.numGuns FROM Classes  WHERE Classes.type='bb')

SELECT CAST(ROUND(AVG(numGuns*1.0), 2) AS NUMERIC(10,2)) AS 'Avg-numGuns' FROM CTE

### Задание: 54
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
С точностью до 2-х десятичных знаков определите среднее число орудий всех линейных кораблей (учесть корабли из таблицы Outcomes).
#### Решение:
WITH CTE AS (
SELECT Outcomes.ship, Classes.numGuns, Classes.type FROM Outcomes JOIN Classes ON Outcomes.ship = Classes.class
UNION
SELECT Ships.name, Classes.numGuns, Classes.type FROM Ships JOIN Classes ON Ships.class = Classes.class)

SELECT CAST(AVG(CTE.numGuns*1.0) AS NUMERIC(6,2)) AS AVG FROM CTE WHERE CTE.type = 'bb'

### Задание: 55
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Для каждого класса определите год, когда был спущен на воду первый корабль этого класса. Если год спуска на воду головного корабля неизвестен, определите минимальный год спуска на воду кораблей этого класса. Вывести: класс, год.
#### Решение:
SELECT Classes.class, min(Ships.launched) FROM Classes LEFT JOIN Ships ON Classes.class = Ships.class GROUP BY Classes.class

### Задание: 56
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Для каждого класса определите число кораблей этого класса, потопленных в сражениях. Вывести: класс и число потопленных кораблей.
#### Решение:
WITH CTE AS (
SELECT Outcomes.ship, Ships.class FROM Outcomes
LEFT JOIN Ships ON Ships.name = Outcomes.ship
WHERE Outcomes.result = 'sunk')

SELECT Classes.class, COUNT(CTE.ship) FROM Classes
LEFT JOIN CTE ON CTE.class = Classes.class OR CTE.ship = Classes.class
GROUP BY Classes.class

### Задание: 57
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Для классов, имеющих потери в виде потопленных кораблей и не менее 3 кораблей в базе данных, вывести имя класса и число потопленных кораблей.
#### Решение:
WITH CTE AS (
SELECT Ships.name, Ships.class FROM Ships
UNION
SELECT Outcomes.ship, Outcomes.ship FROM Outcomes),

CTE2 AS (
SELECT CTE.name AS name, CTE.class AS class,
CASE WHEN Outcomes.result = 'sunk' THEN 1 ELSE 0 END AS sunked
FROM CTE LEFT JOIN Outcomes ON CTE.name = Outcomes.ship)

SELECT Classes.class, SUM(CTE2.sunked) AS sunken FROM Classes
LEFT JOIN CTE2 ON CTE2.class = Classes.class GROUP BY Classes.class
HAVING COUNT(DISTINCT CTE2.name) >= 3 AND SUM(CTE2.sunked) > 0

### Задание: 58
Краткая информация о базе данных "Компьютерная фирма":
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Для каждого типа продукции и каждого производителя из таблицы Product c точностью до двух десятичных знаков найти процентное отношение числа моделей данного типа данного производителя к общему числу моделей этого производителя.
Вывод: maker, type, процентное отношение числа моделей данного типа к общему числу моделей производителя
#### Решение:
WITH zeros AS (
SELECT DISTINCT Product.maker, 'PC' AS 'type', 0 AS 'prc' FROM Product
UNION ALL
SELECT DISTINCT Product.maker, 'Laptop' AS 'type', 0 AS 'prc' FROM Product
UNION ALL
SELECT DISTINCT Product.maker, 'Printer' AS 'type', 0 AS 'prc' FROM Product),

chislo AS (
SELECT Product.maker, COUNT(Product.model) AS 'cntm' FROM Product 
GROUP BY Product.maker),

fin AS (
SELECT Product.maker, Product.type, CAST(COUNT(Product.model)*1.0/chislo.cntm*100 AS NUMERIC(6,2)) AS 'prc' FROM Product LEFT JOIN chislo ON Product.maker=chislo.maker GROUP BY Product.type, Product.maker, chislo.cntm)

SELECT zeros.maker, zeros.type, COALESCE(fin.prc, zeros.prc) FROM fin RIGHT JOIN zeros ON zeros.maker=fin.maker AND zeros.type=fin.type

### Задание: 59
Краткая информация о базе данных "Фирма вторсырья":
Income_o(point, date, inc)
Outcome_o(point, date, out)
Income(code, point, date, inc)
Outcome(code, point, date, out)
Посчитать остаток денежных средств на каждом пункте приема для базы данных с отчетностью не чаще одного раза в день. Вывод: пункт, остаток.
#### Решение:
WITH CTE AS (SELECT Income_o.point, SUM(Income_o.inc) AS 'sum' FROM Income_o
GROUP BY Income_o.point),

CTE2 AS (SELECT Outcome_o.point, SUM(Outcome_o.out) AS 'sum' FROM Outcome_o
GROUP BY Outcome_o.point)

SELECT CTE.point, CTE.sum-COALESCE(CTE2.sum, 0) AS Remain
FROM CTE LEFT JOIN CTE2 ON CTE.point=CTE2.point

### Задание: 60
Краткая информация о базе данных "Фирма вторсырья":
Income_o(point, date, inc)
Outcome_o(point, date, out)
Income(code, point, date, inc)
Outcome(code, point, date, out)
Посчитать остаток денежных средств на начало дня 15/04/01 на каждом пункте приема для базы данных с отчетностью не чаще одного раза в день. Вывод: пункт, остаток.
Замечание. Не учитывать пункты, информации о которых нет до указанной даты.
#### Решение:
WITH CTE AS (SELECT Income_o.point, SUM(Income_o.inc) AS 'sum' FROM Income_o
 WHERE Income_o.date<'2001-04-15' GROUP BY Income_o.point),

CTE2 AS (SELECT Outcome_o.point, SUM(Outcome_o.out) AS 'sum' FROM Outcome_o
 WHERE Outcome_o.date<'2001-04-15' GROUP BY Outcome_o.point)

SELECT CTE.point, CTE.sum-COALESCE(CTE2.sum, 0) AS Remain
FROM CTE LEFT JOIN CTE2 ON CTE.point=CTE2.point

### Задание: 61
Краткая информация о базе данных "Фирма вторсырья":
Income_o(point, date, inc)
Outcome_o(point, date, out)
Income(code, point, date, inc)
Outcome(code, point, date, out)
Посчитать остаток денежных средств на всех пунктах приема для базы данных с отчетностью не чаще одного раза в день.
#### Решение:
WITH CTE AS (SELECT Income_o.point, SUM(Income_o.inc) AS 'sum' FROM Income_o
GROUP BY Income_o.point),

CTE2 AS (SELECT Outcome_o.point, SUM(Outcome_o.out) AS 'sum' FROM Outcome_o
GROUP BY Outcome_o.point),

CTE3 AS (SELECT CTE.point, CTE.sum-COALESCE(CTE2.sum, 0) AS 'summa'
FROM CTE LEFT JOIN CTE2 ON CTE.point=CTE2.point)

SELECT SUM(CTE3.summa) AS Remain FROM CTE3

### Задание: 62
Краткая информация о базе данных "Фирма вторсырья":
Income_o(point, date, inc)
Outcome_o(point, date, out)
Income(code, point, date, inc)
Outcome(code, point, date, out)
Посчитать остаток денежных средств на всех пунктах приема на начало дня 15/04/01 для базы данных с отчетностью не чаще одного раза в день.
#### Решение:
WITH CTE AS (SELECT Income_o.point, SUM(Income_o.inc) AS 'sum' FROM Income_o
 WHERE Income_o.date<'2001-04-15' GROUP BY Income_o.point),

CTE2 AS (SELECT Outcome_o.point, SUM(Outcome_o.out) AS 'sum' FROM Outcome_o
 WHERE Outcome_o.date<'2001-04-15' GROUP BY Outcome_o.point),

CTE3 AS (SELECT CTE.point, CTE.sum-COALESCE(CTE2.sum, 0) AS 'summa'
FROM CTE LEFT JOIN CTE2 ON CTE.point=CTE2.point)

SELECT SUM(CTE3.summa) AS Remain FROM CTE3

### Задание: 63
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Определить имена разных пассажиров, когда-либо летевших на одном и том же месте более одного раза.
#### Решение:
WITH CTE AS (
SELECT Pass_in_trip.ID_psg FROM Pass_in_trip GROUP BY Pass_in_trip.place, Pass_in_trip.ID_psg HAVING COUNT(*)>1)

SELECT Passenger.name FROM Passenger WHERE Passenger.ID_psg IN (SELECT * FROM CTE)

### Задание: 64
Краткая информация о базе данных "Фирма вторсырья":
Income_o(point, date, inc)
Outcome_o(point, date, out)
Income(code, point, date, inc)
Outcome(code, point, date, out)
Используя таблицы Income и Outcome, для каждого пункта приема определить дни, когда был приход, но не было расхода и наоборот.
Вывод: пункт, дата, тип операции (inc/out), денежная сумма за день.
#### Решение:
SELECT Income.point, Income.date, 'inc' AS 'operation', SUM(Income.inc) AS 'money_sum' FROM Income WHERE NOT EXISTS (SELECT Outcome.point, Outcome.date FROM Outcome WHERE Outcome.point=Income.point AND Outcome.date =Income.date) GROUP BY Income.point, Income.date
UNION
SELECT Outcome.point, Outcome.date, 'out' AS 'operation', SUM(Outcome.out) AS 'money_sum' FROM Outcome WHERE NOT EXISTS (SELECT Income.point, Income.date FROM Income WHERE Income.point=Outcome.point AND Income.date =Outcome.date)  GROUP BY Outcome.point, Outcome.date

### Задание: 65
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Пронумеровать уникальные пары {maker, type} из Product, упорядочив их следующим образом:
- имя производителя (maker) по возрастанию;
- тип продукта (type) в порядке PC, Laptop, Printer.
Если некий производитель выпускает несколько типов продукции, то выводить его имя только в первой строке;
остальные строки для ЭТОГО производителя должны содержать пустую строку символов ('').
#### Решение:
WITH CTE AS (
SELECT Product.maker, Product.type, 
CASE WHEN Product.type='PC' THEN 0 
     WHEN Product.type='Laptop' THEN 1 ELSE 2 END AS zero_one_two,
CASE WHEN Product.type='Laptop' AND (Product.maker in (SELECT Product.maker FROM Product WHERE Product.type='PC')) THEN ''
     WHEN Product.type='Printer' AND ((Product.maker in (SELECT Product.maker FROM Product WHERE Product.type='PC')) 
     OR (Product.maker in (SELECT Product.maker FROM Product WHERE Product.type='Laptop'))) THEN '' ELSE Product.maker END AS maker_or_empty
  FROM Product GROUP BY Product.maker, Product.type)

SELECT row_number() OVER(ORDER BY maker, zero_one_two) AS num, maker_or_empty AS maker, CTE.type FROM CTE ORDER BY CTE.maker, zero_one_two

### Задание: 66
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Для всех дней в интервале с 01/04/2003 по 07/04/2003 определить число рейсов из Rostov.
Вывод: дата, количество рейсов
#### Решение:
WITH CTE AS (SELECT '2003-04-01' AS 'date',0 AS 'Qty'
UNION ALL
SELECT '2003-04-02' AS 'date',0 AS 'Qty'
UNION ALL
SELECT '2003-04-03' AS 'date',0 AS 'Qty'
UNION ALL
SELECT '2003-04-04' AS 'date',0 AS 'Qty'
UNION ALL
SELECT '2003-04-05' AS 'date',0 AS 'Qty'
UNION ALL
SELECT '2003-04-06' AS 'date',0 AS 'Qty'
UNION ALL
SELECT '2003-04-07' AS 'date',0 AS 'Qty'
UNION ALL
SELECT Pass_in_trip.date, COUNT(DISTINCT Trip.trip_no) AS 'Qty' FROM Trip RIGHT JOIN Pass_in_trip ON Trip.trip_no=Pass_in_trip.trip_no WHERE Trip.town_from='Rostov' AND Pass_in_trip.date>='2003-04-01' AND Pass_in_trip.date<='2003-04-07' GROUP BY Trip.town_from, Pass_in_trip.date)

SELECT CTE.date, MAX(CTE.Qty) AS Qty FROM CTE GROUP BY CTE.date

### Задание: 67
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Найти количество маршрутов, которые обслуживаются наибольшим числом рейсов.
Замечания.
1) A - B и B - A считать РАЗНЫМИ маршрутами.
2) Использовать только таблицу Trip
#### Решение:
WITH CTE AS (SELECT TOP 1 WITH TIES COUNT(*) cnt, Trip.town_from, Trip.town_to FROM Trip GROUP BY Trip.town_from, Trip.town_to ORDER BY cnt DESC)

SELECT COUNT(*) AS qty FROM CTE

### Задание: 68
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Найти количество маршрутов, которые обслуживаются наибольшим числом рейсов.
Замечания.
1) A - B и B - A считать ОДНИМ И ТЕМ ЖЕ маршрутом.
2) Использовать только таблицу Trip
#### Решение:
WITH CTE AS (
SELECT COUNT(*) cnt, Trip.town_from town1, Trip.town_to town2 FROM Trip WHERE Trip.town_from >= Trip.town_to
GROUP BY Trip.town_from, Trip.town_to 
UNION ALL
SELECT COUNT(*) cnt, Trip.town_to, Trip.town_from FROM Trip WHERE Trip.town_to > Trip.town_from GROUP BY Trip.town_from, Trip.town_to
),

CTE2 AS (
SELECT TOP 1 WITH TIES SUM(CTE.cnt) sum_cnt, CTE.town1, CTE.town2 FROM CTE GROUP BY CTE.town1, CTE.town2 ORDER BY sum_cnt DESC
)

SELECT COUNT(*) FROM CTE2

### Задание: 69
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
По таблицам Income и Outcome для каждого пункта приема найти остатки денежных средств на конец каждого дня,
в который выполнялись операции по приходу и/или расходу на данном пункте.
Учесть при этом, что деньги не изымаются, а остатки/задолженность переходят на следующий день.
Вывод: пункт приема, день в формате "dd/mm/yyyy", остатки/задолженность на конец этого дня.
#### Решение:
WITH CTE AS
(
  SELECT Income.point, Income.date, Income.inc, 0 AS "out" FROM Income
  UNION ALL
  SELECT Outcome.point, Outcome.date, 0 AS inc, Outcome.out FROM Outcome
)

SELECT CTE.point, CONVERT(VARCHAR, CTE.date, 103) AS day,
 ( SELECT SUM(i.inc) FROM CTE i WHERE i.date <= CTE.date AND i.point = CTE.point )
-
( SELECT SUM(i.out) FROM CTE i WHERE i.date <= CTE.date AND i.point = CTE.point ) AS rem
FROM CTE GROUP BY CTE.point, CTE.date

### Задание: 70
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Укажите сражения, в которых участвовало по меньшей мере три корабля одной и той же страны.
#### Решение:
SELECT DISTINCT Outcomes.battle FROM Outcomes 
LEFT JOIN Ships ON Ships.name = Outcomes.ship
LEFT JOIN Classes ON Outcomes.ship = Classes.class OR Ships.class = Classes.class
WHERE Classes.country IS NOT NULL
GROUP BY Classes.country, Outcomes.battle
HAVING COUNT(Outcomes.ship) >= 3

### Задание: 71
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найти тех производителей ПК, все модели ПК которых имеются в таблице PC.
#### Решение:
SELECT DISTINCT Product.maker FROM Product, PC WHERE Product.type='PC' AND Product.model IN (SELECT PC.model FROM PC)
EXCEPT
SELECT DISTINCT Product.maker FROM Product, PC WHERE Product.type='PC' AND Product.model NOT IN (SELECT PC.model FROM PC)

### Задание: 72
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Среди тех, кто пользуется услугами только какой-нибудь одной компании, определить имена разных пассажиров, летавших чаще других.
Вывести: имя пассажира и число полетов.
#### Решение:
WITH CTE AS (
SELECT Pass_in_trip.ID_psg, Trip.ID_comp, COUNT(*) cnt FROM Pass_in_trip
JOIN Trip ON Trip.trip_no=Pass_in_trip.trip_no
GROUP BY Pass_in_trip.ID_psg, Trip.ID_comp
),

CTE2 AS (SELECT CTE.ID_psg, MAX(CTE.cnt) cnt FROM CTE GROUP BY CTE.ID_psg HAVING COUNT(*)=1)

SELECT TOP 1 WITH TIES Passenger.name, CTE2.cnt FROM Passenger JOIN CTE2 ON Passenger.ID_psg=CTE2.ID_psg ORDER BY cnt DESC

### Задание: 73
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Для каждой страны определить сражения, в которых не участвовали корабли данной страны.
Вывод: страна, сражение
#### Решение:
SELECT DISTINCT Classes.country, Battles.name
FROM Battles, Classes
EXCEPT
SELECT Classes.country, Outcomes.battle
FROM Outcomes
LEFT JOIN Ships ON Ships.name = Outcomes.ship
LEFT JOIN Classes ON Outcomes.ship = Classes.class OR Ships.class = Classes.class
WHERE Classes.country IS NOT NULL
GROUP BY Classes.country, Outcomes.battle

### Задание: 74
Краткая информация о базе данных "Корабли":
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Вывести классы всех кораблей России (Russia). Если в базе данных нет классов кораблей России, вывести классы для всех имеющихся в БД стран.
Вывод: страна, класс
#### Решение:
WITH CTE AS (SELECT Classes.country, Classes.class FROM Classes WHERE Classes.country = 'Russia')

SELECT Classes.country, Classes.class FROM Classes
WHERE Classes.country = 'Russia' AND EXISTS (SELECT * FROM CTE)
UNION ALL
SELECT Classes.country, Classes.class FROM Classes
WHERE NOT EXISTS (SELECT * FROM CTE)

### Задание: 75
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Для тех производителей, у которых есть продукты с известной ценой хотя бы в одной из таблиц Laptop, PC, Printer найти максимальные цены на каждый из типов продукции.
Вывод: maker, максимальная цена на ноутбуки, максимальная цена на ПК, максимальная цена на принтеры.
Для отсутствующих продуктов/цен использовать NULL.
#### Решение:
SELECT
  Product.maker,
  MAX(Laptop.price) AS laptop,
  MAX(PC.price) AS pc,
  MAX(Printer.price) AS printer
FROM
  Product
LEFT JOIN Laptop ON Product.model=Laptop.model
LEFT JOIN PC ON Product.model=PC.model
LEFT JOIN Printer ON Product.model=Printer.model
GROUP BY Product.maker
HAVING
  MAX(Laptop.price) IS NOT NULL
  OR MAX(PC.price) IS NOT NULL
  OR MAX(Printer.price) IS NOT NULL

### Задание: 76
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Определить время, проведенное в полетах, для пассажиров, летавших всегда на разных местах. Вывод: имя пассажира, время в минутах.
#### Решение:
WITH CTE AS (
SELECT ROW_NUMBER() OVER (PARTITION BY Passenger.ID_psg, Pass_in_trip.place ORDER BY Pass_in_trip.date) AS row_number,
DATEDIFF (minute, time_out, DATEADD(DAY,IIF(time_in<time_out,1,0), time_in)) AS minutes, Passenger.Id_psg, Passenger.name
FROM Pass_in_trip LEFT JOIN Trip ON Pass_in_trip.trip_no = Trip.trip_no
LEFT JOIN Passenger ON Passenger.ID_psg = Pass_in_trip.ID_psg)

SELECT MAX(CTE.name) AS name, SUM(CTE.minutes) AS minutes FROM CTE
GROUP BY CTE.ID_psg HAVING MAX(CTE.row_number) = 1

### Задание: 77
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Определить дни, когда было выполнено максимальное число рейсов из
Ростова ('Rostov'). Вывод: число рейсов, дата.
#### Решение:
WITH CTE AS (SELECT COUNT(DISTINCT(Pass_in_trip.trip_no)) AS Qty, Pass_in_trip.date FROM Trip, Pass_in_trip WHERE Trip.trip_no=Pass_in_trip.trip_no AND Trip.town_from = 'Rostov' GROUP BY Pass_in_trip.date)

SELECT TOP 1 WITH TIES * FROM CTE ORDER BY CTE.Qty DESC

### Задание: 78
Имеются следующие отношения:
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Для каждого сражения определить первый и последний день месяца в котором оно состоялось.
Вывод: сражение, первый день месяца, последний день месяца.
Замечание: даты представить без времени в формате "yyyy-mm-dd".
#### Решение:
SELECT DISTINCT Battles.name, 
CONVERT(VARCHAR, DATEADD(m, DATEDIFF(m,0,Battles.date),0), 23), 
CONVERT(VARCHAR, DATEADD(s,-1,DATEADD(m, DATEDIFF(m,0,Battles.date)+1,0)), 23) FROM Battles

### Задание: 79
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Определить пассажиров, которые больше других времени провели в полетах.
Вывод: имя пассажира, общее время в минутах, проведенное в полетах
#### Решение:
WITH CTE AS (
SELECT ROW_NUMBER() OVER (PARTITION BY Passenger.ID_psg, Pass_in_trip.place ORDER BY Pass_in_trip.date) AS row_number,
DATEDIFF (minute, time_out, DATEADD(DAY,IIF(time_in<time_out,1,0), time_in)) AS time_in_min, Passenger.Id_psg, Passenger.name
FROM Pass_in_trip LEFT JOIN Trip ON Pass_in_trip.trip_no = Trip.trip_no
LEFT JOIN Passenger ON Passenger.ID_psg = Pass_in_trip.ID_psg)

SELECT TOP 1 WITH TIES MAX(CTE.name) AS name, SUM(time_in_min) AS time_in_min FROM CTE GROUP BY CTE.ID_psg ORDER BY time_in_min DESC

### Задание: 80
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найти производителей любой компьютерной техники, у которых нет моделей ПК, не представленных в таблице PC.
#### Решение:
WITH CTE AS (
SELECT Product.maker FROM Product WHERE Product.type='PC' AND Product.model NOT IN (SELECT PC.model FROM PC))

SELECT DISTINCT Product.maker FROM Product WHERE Product.maker NOT IN (SELECT * FROM CTE)

### Задание: 81
Краткая информация о базе данных "Фирма вторсырья":
Income_o(point, date, inc)
Outcome_o(point, date, out)
Income(code, point, date, inc)
Outcome(code, point, date, out)
Из таблицы Outcome получить все записи за тот месяц (месяцы), с учетом года, в котором суммарное значение расхода (out) было максимальным.
#### Решение:
WITH vm AS (
SELECT TOP 1 WITH TIES CONVERT(VARCHAR, DATEADD(m, DATEDIFF(m,0,Outcome.date),0), 23) mnth, 
SUM(Outcome.out) sm FROM Outcome GROUP BY CONVERT(VARCHAR, DATEADD(m, DATEDIFF(m,0,Outcome.date),0), 23) ORDER BY SUM(Outcome.out) DESC), 

vmonth AS (
SELECT vm.mnth FROM vm)

SELECT Outcome.code, Outcome.point, Outcome.date, Outcome.out FROM Outcome, vmonth WHERE CONVERT(VARCHAR, DATEADD(m, DATEDIFF(m,0,Outcome.date),0), 23) = vmonth.mnth

### Задание: 82
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
В наборе записей из таблицы PC, отсортированном по столбцу code (по возрастанию) найти среднее значение цены для каждой шестерки подряд идущих ПК.
Вывод: значение code, которое является первым в наборе из шести строк, среднее значение цены в наборе.
#### Решение:
WITH CTE AS (SELECT PC.code,PC.price, number= ROW_NUMBER() OVER (ORDER BY PC.code) FROM PC)

SELECT CTE.code, AVG(c.price) AS avgprс FROM CTE 
JOIN CTE c ON (c.number-CTE.number)<6 AND (c.number-CTE.number)> =0
GROUP BY CTE.number, CTE.code HAVING COUNT(CTE.number)=6

### Задание: 83
Имеются следующие отношения:
Classes (class, type, country, numGuns, bore, displacement)
Ships (name, class, launched)
Battles (name, date)
Outcomes (ship, battle, result)
Определить названия всех кораблей из таблицы Ships, которые удовлетворяют, по крайней мере, комбинации любых четырёх критериев из следующего списка:
numGuns = 8
bore = 15
displacement = 32000
type = bb
launched = 1915
class=Kongo
country=USA
#### Решение:
SELECT Ships.name FROM Ships JOIN Classes ON Ships.class = Classes.class
WHERE
CASE WHEN Classes.numGuns = 8 THEN 1 ELSE 0 END +
CASE WHEN Classes.bore = 15 THEN 1 ELSE 0 END +
CASE WHEN Classes.displacement = 32000 THEN 1 ELSE 0 END +
CASE WHEN Classes.type = 'bb' THEN 1 ELSE 0 END +
CASE WHEN Ships.launched = 1915 THEN 1 ELSE 0 END +
CASE WHEN Ships.class = 'Kongo' THEN 1 ELSE 0 END +
CASE WHEN Classes.country = 'USA' THEN 1 ELSE 0 END > = 4

### Задание: 84
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Для каждой компании подсчитать количество перевезенных пассажиров (если они были в этом месяце) по декадам апреля 2003. При этом учитывать только дату вылета.
Вывод: название компании, количество пассажиров за каждую декаду
#### Решение:
WITH CTE AS (
SELECT Trip.ID_comp,
       SUM(CASE WHEN DAY(Pass_in_trip.date) < 11 THEN 1 ELSE 0 END) AS "1-10",
       SUM(CASE WHEN (DAY(Pass_in_trip.date) > 10 AND DAY(Pass_in_trip.date) < 21) THEN 1 ELSE 0 END) AS "11-20",
       SUM(CASE WHEN DAY(Pass_in_trip.date) > 20 THEN 1 ELSE 0 END) AS "21-30" FROM Trip JOIN Pass_in_trip ON Trip.trip_no = Pass_in_trip.trip_no AND CONVERT(CHAR(6), Pass_in_trip.date, 112) = '200304' GROUP BY Trip.ID_comp)

SELECT Company.name, CTE."1-10", CTE."11-20", CTE."21-30"
FROM CTE JOIN Company ON CTE.ID_comp = Company.ID_comp

### Задание: 85
Исходная база данных: "Компьютерная фирма".
Product(maker, model, type)
PC(code, model, speed, ram, hd, cd, price)
Laptop(code, model, speed, ram, hd, price, screen)
Printer(code, model, color, type, price)
Найти производителей, которые выпускают только принтеры или только PC.
При этом искомые производители PC должны выпускать не менее 3 моделей.
#### Решение:
SELECT Product.maker FROM Product GROUP BY Product.maker
HAVING COUNT(DISTINCT Product.type) = 1 AND (MIN(Product.type) = 'Printer' OR (MIN(Product.type) = 'PC' AND COUNT(Product.model) >= 3))

### Задание: 86
Для каждого производителя перечислить в алфавитном порядке с разделителем "/" все типы выпускаемой им продукции.
Вывод: maker, список типов продукции
#### Решение:
SELECT Product.maker, CASE COUNT(DISTINCT Product.type) 
WHEN 1 THEN MAX(Product.type)
WHEN 2 THEN MIN(Product.type) + '/' + MAX(Product.type)
WHEN 3 THEN 'Laptop/PC/Printer' END AS types
FROM Product GROUP BY maker

### Задание: 87
Краткая информация о базе данных "Аэрофлот":
Company (ID_comp, name)
Trip(trip_no, ID_comp, plane, town_from, town_to, time_out, time_in)
Passenger(ID_psg, name)
Pass_in_trip(trip_no, date, ID_psg, place)
Считая, что пункт самого первого вылета пассажира является местом жительства, найти не москвичей, которые прилетали в Москву более одного раза.
Вывод: имя пассажира, количество полетов в Москву
#### Решение:
WITH CTE AS (
SELECT MIN (date+time_out) AS min FROM Trip JOIN Pass_in_trip ON Trip.trip_no = Pass_in_trip.trip_no),

CTE2 AS (
SELECT DISTINCT Pass_in_trip.ID_psg FROM Trip 
JOIN Pass_in_trip ON Trip.trip_no = Pass_in_trip.trip_no 
WHERE Pass_in_trip.date+Trip.time_out = (SELECT * FROM CTE) AND Trip.town_from = 'Moscow')

SELECT DISTINCT Passenger.name, COUNT(Trip.town_to) Qty
FROM Trip JOIN Pass_in_trip ON Trip.trip_no = Pass_in_trip.trip_no 
JOIN Passenger ON Pass_in_trip.ID_psg = Passenger.ID_psg 
WHERE Trip.town_to = 'Moscow' AND Pass_in_trip.ID_psg NOT IN (SELECT * FROM CTE2)
GROUP BY Pass_in_trip.ID_psg, Passenger.name HAVING COUNT(Trip.town_to) > 1
