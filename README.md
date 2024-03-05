# Домашнее задание к занятию "`SQL. Часть 2`" - `Савин Алексей`

## Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:  

фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### Решение 1  

```
select concat(sotr.first_name , ' ', sotr.last_name) as сотрудник,  c2.city as город, COUNT(c.customer_id) as "покупатели"
from staff sotr
join store s2 on s2.store_id = sotr.store_id 
join customer c on c.store_id = s2.store_id
join address a on a.address_id = s2.address_id 
join city c2 on c2.city_id = a.city_id 
group by sotr.staff_id, c2.city_id 
having COUNT(c.customer_id) > 300;
```
![part1](https://github.com/AI-Savin/hw_SQL_2/blob/main/img/part1.png)    
  
---

## Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.  

### Решение 2  
```
select count(film_id) as "кол-во фильмов" from film 
where length > (select AVG(length) from film);
```
![part2](https://github.com/AI-Savin/hw_SQL_2/blob/main/img/part2.png)   

 ---

## Задание 3  
 Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц. 

 ### Решение 3  
добавил группировку по году
 ```
SELECT DATE_FORMAT(p.payment_date, '%M, %Y') AS месяц, SUM(p.amount) AS сумма_платежей, COUNT(p.rental_id) AS количество_аренд
FROM payment p 
GROUP BY месяц
ORDER BY сумма_платежей LIMIT 1;
```
![part3_1](https://github.com/AI-Savin/hw_SQL_2/blob/main/img/part3_1.png)  

 ---
 
