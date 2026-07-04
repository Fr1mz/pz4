\# GraphRAG Titanic SQL Agent



\## Тема



GraphRAG-архитектура для SQL-агента, который отвечает на вопросы пользователя по данным Titanic через граф знаний, граф агентов и RAG-поиск.



\## Домен



В качестве рабочего домена выбран датасет Titanic.  

Он содержит сведения о пассажирах, билетах, каютах, классе обслуживания, поле, возрасте, стоимости билета и факте выживания.



\## Источники данных



\- Titanic dataset / passengers.csv

\- Описание таблицы passengers

\- Описание полей: survived, pclass, sex, age, fare, cabin, embarked

\- Бизнес-термины: пассажир, класс обслуживания, выживание, порт посадки

\- Примеры SQL-запросов



\## Граф знаний



В графе знаний используются доменные сущности:



\- Passenger

\- Ticket

\- Cabin

\- SurvivalStatus

\- PassengerClass

\- EmbarkationPort

\- FamilyGroup

\- AnalyticalMetric



Связи:



\- Passenger HAS\_TICKET Ticket

\- Passenger STAYED\_IN Cabin

\- Passenger HAS\_CLASS PassengerClass

\- Passenger HAS\_SURVIVAL\_STATUS SurvivalStatus

\- Passenger EMBARKED\_AT EmbarkationPort

\- Passenger BELONGS\_TO FamilyGroup



\## Граф агентов



В архитектуре используются агенты:



\- Router Agent — определяет тип запроса пользователя

\- GraphRAG Retriever — ищет релевантный контекст

\- Graph Agent — работает с графом знаний

\- Cypher Agent — формирует запросы к графу

\- SQL Agent — формирует SQL-запрос

\- SQL Grader — проверяет корректность SQL

\- Security Guard — проверяет безопасность запроса

\- Answer Agent — формирует итоговый ответ



\## Слой аналитики



В системе предусмотрен слой графовой аналитики:



\- PageRank — определение наиболее значимых сущностей

\- Community Detection — поиск групп связанных сущностей

\- Path Search — поиск маршрутов между таблицами и сущностями



\## End-to-end пример



Вопрос пользователя:



> Сколько выживших пассажиров было в каждом классе?



Ход обработки:



1\. Router Agent определяет, что вопрос аналитический.

2\. GraphRAG Retriever ищет релевантные сущности и поля.

3\. Система находит таблицу passengers и поля survived, pclass.

4\. Graph Agent уточняет связь между понятием "класс" и полем pclass.

5\. SQL Agent формирует SQL-запрос.

6\. SQL Grader проверяет корректность.

7\. Security Guard проверяет, что запрос безопасный.

8\. SQL выполняется в БД.

9\. Answer Agent возвращает результат пользователю.



Пример SQL:



```sql

SELECT pclass, COUNT(\*) AS survived\_count

FROM passengers

WHERE survived = 1

GROUP BY pclass

ORDER BY pclass;

