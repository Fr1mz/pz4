\# Demo Scenario



\## Пользовательский запрос



Сколько выживших пассажиров было в каждом классе?



\## Найденный GraphRAG-контекст



\- Доменная сущность: Passenger

\- Метрика: SurvivalStatus

\- Поле таблицы: survived

\- Поле таблицы: pclass

\- Таблица: passengers



\## Сформированный SQL



```sql

SELECT pclass, COUNT(\*) AS survived\_count

FROM passengers

WHERE survived = 1

GROUP BY pclass

ORDER BY pclass;

