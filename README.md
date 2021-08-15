# Sql-ex.ru
Решение заданий с sql-ex.ru
<h3>Задание: 1</h3>
Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd
<b>Запрос: 1</b>
SELECT DISTINCT model, speed, hd FROM PC WHERE price < '500';
