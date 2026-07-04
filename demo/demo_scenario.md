# Demo Scenario

## Пользовательский запрос

Сколько выживших пассажиров было в каждом классе?

## Найденный GraphRAG-контекст

- Доменная сущность: Passenger
- Метрика: SurvivalStatus
- Таблица: passengers
- Поле таблицы: survived
- Поле таблицы: pclass

## Сформированный SQL

```sql
SELECT pclass, COUNT(*) AS survived_count
FROM passengers
WHERE survived = 1
GROUP BY pclass
ORDER BY pclass;
```

## Ожидаемый результат

Система возвращает количество выживших пассажиров по каждому классу обслуживания.

## End-to-end ход обработки

1. Пользователь задаёт вопрос на естественном языке.
2. Router Agent определяет, что это аналитический SQL-запрос.
3. GraphRAG Retriever ищет релевантный контекст.
4. Graph Agent уточняет связь между сущностью Passenger и полями таблицы passengers.
5. Cypher Agent может использовать граф знаний для поиска связанных сущностей.
6. SQL Agent формирует SQL-запрос.
7. SQL Grader проверяет корректность SQL.
8. Security Guard проверяет ограничения: SELECT-only, права доступа, LIMIT.
9. SQL выполняется в базе данных.
10. Answer Agent возвращает результат пользователю.