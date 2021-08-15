# Sql-ex.ru
Решение заданий с sql-ex.ru
<h3>Задание: 1</h3>
Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd
<h3>Запрос: 1</h3>
SELECT DISTINCT model, speed, hd FROM PC WHERE price < '500';
