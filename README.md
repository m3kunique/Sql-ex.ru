# Sql-ex.ru
<h2>Решение заданий с sql-ex.ru</h2>
<h3>Задание 1:</h3>
Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd<br>
<b>Запрос 1:</b><br>
SELECT DISTINCT model, speed, hd FROM PC WHERE price < '500';
<h3>Задание 2:</h3>
Найдите производителей принтеров. Вывести: maker<br>
<b>Запрос 2:</b><br>
SELECT DISTINCT maker FROM Product WHERE type = 'Printer';
<h3>Задание 3:</h3>
Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.<br>
<b>Запрос 3:</b><br>
SELECT ALL model, ram, screen FROM Laptop WHERE price > 1000;
<h3>Задание 4:</h3>
Найдите все записи таблицы Printer для цветных принтеров.<br>
<b>Запрос 4:</b><br>
SELECT * FROM Printer WHERE color = 'y';
<h3>Задание 5:</h3>
Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.<br>
<b>Запрос 5:</b><br>
SELECT model, speed, hd FROM PC WHERE cd = '12x' AND price < '600' OR cd = '24x' AND price < '600';
<h3>Задание 6:</h3>
Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.<br>
<b>Запрос 6:</b><br>
SELECT DISTINCT Product.maker, Laptop.speed FROM Product INNER JOIN Laptop ON Product.model = Laptop.model AND Laptop.hd >= 10;
<h3>Задание 7:</h3>
Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).<br>
<b>Запрос 7:</b><br>
SELECT Laptop.model, Laptop.price FROM Laptop INNER JOIN Product ON Laptop.model = Product.model;<br> 
WHERE Product.maker= 'B'<br> 
UNION<br>
SELECT PC.model, PC.price FROM PC INNER JOIN Product ON PC.model = Product.model;<br>  
WHERE Product.maker= 'B'<br>
UNION<br>
SELECT Printer.model, Printer.price FROM Printer INNER JOIN Product ON Printer.model = Product.model;<br>
WHERE Product.maker= 'B'<br>
<h3>Задание 8:</h3>
Найдите производителя, выпускающего ПК, но не ПК-блокноты.<br>
<b>Запрос 8:</b><br>
SELECT maker FROM Product WHERE type = 'PC' EXCEPT SELECT maker FROM Product WHERE type = 'Laptop';
<h3>Задание 9:</h3>
Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker<br>
<b>Запрос 9:</b><br>
SELECT DISTINCT Product.maker FROM Product INNER JOIN PC ON Product.model = PC.model AND PC.speed >= 450;
<h3>Задание 10:</h3>
Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price<br>
<b>Запрос 10:</b><br>
SELECT model, price FROM Printer WHERE price IN (SELECT MAX(price) FROM Printer;
<h3>Задание 11:</h3>
Найдите среднюю скорость ПК.<br>
<b>Запрос 11:</b><br>
SELECT AVG(speed) FROM PC;
<h3>Задание 12:</h3>
Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.<br>
<b>Запрос 12:</b><br>
SELECT AVG(speed) FROM Laptop WHERE price > 1000;
<h3>Задание 13:</h3>
Найдите среднюю скорость ПК, выпущенных производителем A.<br>
<b>Запрос 13:</b><br>
SELECT AVG(PC.speed) FROM PC INNER JOIN Product ON PC.model = Product.model AND maker = 'A';
<h3>Задание 14:</h3>
Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.<br>
<b>Запрос 14:</b><br>
SELECT Ships.class, Ships.name, Classes.country FROM Ships INNER JOIN Classes ON Ships.class = Classes.class WHERE Classes.numGuns >=10;
<h3>Задание 15:</h3>
Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD<br>
<b>Запрос 15:</b><br>
SELECT hd FROM PC GROUP BY hd HAVING COUNT(model) >= 2;
<h3>Задание 16:</h3>
Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.<br>
<b>Запрос 16:</b><br>
SELECT DISTINCT A.model, B.model, A.speed, A.ram FROM pc A, pc B WHERE A.ram = B.ram AND A.speed = B.speed AND A.model > B.model;
<h3>Задание 17:</h3>
Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК. Вывести: type, model, speed<br>
<b>Запрос 17:</b><br>
SELECT DISTINCT p.type, l.model, l.speed<br>
FROM Laptop l, Product p<br>
WHERE speed < ALL (SELECT speed FROM PC)<br>
AND l.model=p.model;
<h3>Задание 18:</h3>
Найдите производителей самых дешевых цветных принтеров. Вывести: maker, price<br>
<b>Запрос 18:</b><br>
SELECT DISTINCT Product.maker, Printer.price<br>
FROM Product, Printer<br>
WHERE Product.model = Printer.model<br>
AND Printer.color = 'Y'<br>
AND Printer.price = (SELECT MIN(p.price)<br>
FROM Printer p<br>
WHERE p.color = 'Y');
<h3>Задание 19:</h3>
Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов. Вывести: maker, средний размер экрана.<br>
<b>Запрос 19:</b><br>
SELECT Product.maker, AVG(Laptop.screen) GROUP BY Product.maker;
<h3>Задание 20:</h3>
Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.<br>
<b>Запрос 20:</b><br>
SELECT maker, COUNT(*) FROM Product WHERE type = 'PC' GROUP BY Product.maker HAVING COUNT(*) >= 3;
<h3>Задание 21:</h3>
Найдите максимальную цену ПК, выпускаемых каждым производителем, у которого есть модели в таблице PC. Вывести: maker, максимальная цена.<br>
<b>Запрос 21:</b><br>
SELECT Product.maker, MAX(PC.price) FROM Product INNER JOIN PC ON Product.model = PC.model GROUP BY Product.maker;
<h3>Задание 22:</h3>
Для каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.<br>
<b>Запрос 22:</b><br>
SELECT speed, AVG(price) FROM PC WHERE speed > 600 GROUP BY speed;
<h3>Задание 23:</h3>
Найдите производителей, которые производили бы как ПК со скоростью не менее 750 МГц, так и ПК-блокноты со скоростью не менее 750 МГц. Вывести: Maker<br>
<b>Запрос 23:</b><br>
SELECT DISTINCT Product.maker<br>
FROM Product INNER JOIN PC ON Product.model = PC.model WHERE PC.speed >=750 AND<br>
Product.maker IN (SELECT Product.maker FROM Laptop INNER JOIN Product ON Laptop.model = Product.model WHERE Laptop.speed >= 750)<br>
GROUP BY Product.maker;
<h3>Задание 24:</h3>
Перечислите номера моделей любых типов, имеющих самую высокую цену по всей имеющейся в базе данных продукции.<br>
<b>Запрос 24:</b><br>
WITH MaxPrice AS (
    SELECT MAX(price) AS max_price
    FROM (
        SELECT price FROM PC
        UNION
        SELECT price FROM Laptop
        UNION
        SELECT price FROM Printer
    ) AS AllPrices
)
SELECT model
FROM (
    SELECT model, price FROM PC
    UNION
    SELECT model, price FROM Laptop
    UNION
    SELECT model, price FROM Printer
) AS AllProducts
WHERE price = (SELECT max_price FROM MaxPrice);
<h3>Задание 25:</h3>
Найдите производителей принтеров, которые производят ПК с наименьшим объемом RAM и с самым быстрым процессором среди всех ПК, имеющих наименьший объем RAM. Вывести: Maker<br>
<b>Запрос 25:</b><br>
SELECT distinct product.maker FROM product WHERE product.type='Printer'<br>
INTERSECT<br>
SELECT DISTINCT Product.maker<br>
FROM Product INNER JOIN PC ON Product.model = PC.model WHERE Product.type = 'PC' AND PC.ram IN (SELECT MIN(PC.ram) FROM PC) AND PC.speed IN (SELECT MAX(PC.speed) FROM PC WHERE PC.ram IN (SELECT MIN(PC.ram) FROM PC));

