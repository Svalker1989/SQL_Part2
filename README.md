# Домашнее задание к занятию "`SQL. Часть 2`" - `Стрекозов Владимир`

### Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:  
фамилия и имя сотрудника из этого магазина;  
город нахождения магазина;  
количество пользователей, закреплённых в этом магазине.  
Запрос:  
`select c.store_id as "Store_ID", count(c.customer_id) as "Clients_count", CONCAT(s2.first_name, ' ',s2.last_name) AS "FI", c2.city as "Store's_city"
from customer c
join store s on c.store_id = s.store_id 
join staff s2 on s.manager_staff_id = s2.staff_id 
join address a on s.address_id = a.address_id 
JOIN city c2 on a.city_id = c2.city_id
group by c.store_id
HAVING count(c.customer_id) > 300;`  
![](https://github.com/Svalker1989/SQL_Part2/blob/main/Z1.PNG)  
### Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.  
Запрос:  
`select count(f.film_id)
from film f 
where f.`length` > (select avg(f2.`length`) from film f2);`  
![](https://github.com/Svalker1989/SQL_Part2/blob/main/Z2.PNG)  
### Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.  
Запрос:  
`SELECT SUBSTR(p.payment_date, 6, 2) as mon, sum(p.amount) as summ, count(p.rental_id) as kol_arend
from payment p 
group by mon
ORDER BY summ DESC limit 1;`  
![](https://github.com/Svalker1989/SQL_Part2/blob/main/Z3.PNG)  
### Задание 4*
Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».  
Запрос:  
`select p.staff_id, count(p.payment_id) as kol_prod,
case 
	when count(p.payment_id) > 8000 then 'yes'
	when count(p.payment_id) < 8000 then 'no'
end as premiya
from payment p 
group by p.staff_id ;`  
![](https://github.com/Svalker1989/SQL_Part2/blob/main/Z4.PNG)  
### Задание 5*
Найдите фильмы, которые ни разу не брали в аренду.  
Запрос:  
`SELECT f.title
FROM film f
LEFT JOIN inventory i ON i.film_id = f.film_id
LEFT JOIN rental r ON r.inventory_id = i.inventory_id
WHERE r.rental_id IS NULL;`  
![](https://github.com/Svalker1989/SQL_Part2/blob/main/Z5.PNG)  
