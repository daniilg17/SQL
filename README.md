# 📌 SQL

**SQL** (Structured Query Language) — это стандартный язык для работы с реляционными базами данных.
Он позволяет QA-инженерам получать тестовые данные, проверять изменения после действий в приложении и убеждаться в корректности данных после разных операций — что делает SQL важнейшим инструментом в ручном и автоматизированном тестировании.

### 📚 Описание таблиц базы данных

#### В этом проекте используются две основные таблицы из [Hogwarts-themed database](https://drive.google.com/drive/u/3/folders/1MC0AttnmlAmugifFlX3hG6pssYZDqpPB):

### Table: `characters`

Содержит информацию о персонажах — их имена, возраст, принадлежность к факультету, патронус и уникальный ID.

| id | first\_name | last\_name | age | faculty    | patronus             | wand\_id |
| -- | ----------- | ---------- | --- | ---------- | -------------------- | -------- |
| 1  | Harry       | Potter     | 11  | Gryffindor | Stag                 | 10       |
| 2  | Hermione    | Granger    | 11  | Gryffindor | Otter                | 9        |
| 3  | Ron         | Weasley    | 11  | Gryffindor | Jack Russell terrier | 8        |
| 4  | Draco       | Malfoy     | 11  | Slytherin  |                      | 6        |
| 5  | Vincent     | Crabbe     | 11  | Slytherin  |                      | 6        |
| 6  | Gregory     | Goyle      | 11  | Slytherin  |                      | 1        |
| 7  | Albus       | Dumbledore | 111 | Gryffindor | Phoenix              | 2        |
| 8  | Luna        | Lovegood   | 11  | Ravenclaw  | Hare                 | 2        |
| 9  | Cedric      | Diggory    | 14  | Hufflepuff | Unknown              | 3        |
| 10 | Severus     | Snape      | 55  | Slytherin  | Doe                  | 4        |
| 11 | Lord        | Voldemort  |     | Slytherin  |                      | 5        |

---

### Table: `library`

Содержит данные о книгах, которые брали персонажи: дата выдачи, дата возврата и номер полки.

| id | character\_id | title                                      | issue\_date | return\_date | shelf\_id |
| -- | ------------- | ------------------------------------------ | ----------- | ------------ | --------- |
| 1  | 6             | Hogwarts: A History                        | 2010-10-20  | 2020-10-20   | 1         |
| 2  | 7             | Quidditch Through The Ages                 | 2010-11-20  | 2020-11-20   | 2         |
| 3  | 9             | The Lockhart Collection                    | 2015-12-20  | 2030-12-20   | 3         |
| 4  | 10            | Moste Potente Potions                      | 2001-01-20  | 2002-01-20   | 4         |
| 5  | 11            | The Life And Lies Of Albus Dumbledore      | 2018-07-20  | 2028-07-20   | 5         |
| 6  | 4             | Fantastic Beasts And Where To Find Them    | 2010-10-20  | 2020-10-20   | 6         |
| 7  | 13            | The Tales Of Beadle The Bard               | 2003-03-20  | 2004-03-20   | 7         |
| 8  | 3             | Advanced Potion-Making                     | 2003-05-20  | 2006-05-20   | 8         |
| 9  | 2             | A History Of Magic                         | 2012-12-20  | 2022-12-20   | 9         |
| 10 | 1             | Magical Water Plants Of The Highland Rocks | 2006-06-20  | 2010-06-20   | 10        |
| 11 | 8             | Quidditch Through The Ages                 | 2010-11-20  | 2020-11-20   | 2         |
| 12 | 12            | Magical Water Plants Of The Highland Rocks | 2010-11-20  | 2020-10-20   | 10        |
| 13 | 5             | Fantastic Beasts And Where To Find Them    | 2006-06-20  | 2010-00-20   | 6         |

## Основные запросы

```sql
SELECT * FROM characters;                                   -- Выбрать все данные из таблицы characters
SELECT first_name, last_name FROM characters;               -- Выбрать только определённые столбцы
SELECT DISTINCT faculty FROM characters;                    -- Получить уникальные значения

SELECT first_name AS "Half-Blood Prince"                    -- Пример псевдонима (alias)
FROM characters WHERE id = 7; 
```

## Фильтрация и сортировка

```sql
SELECT * FROM characters WHERE age > 30;                    -- Фильтр по возрасту (старше 30)
SELECT * FROM characters WHERE last_name LIKE '%a%';        -- Фамилии, содержащие букву "a"
SELECT * FROM characters ORDER BY age DESC;                 -- Сортировка по возрасту (по убыванию)

SELECT * FROM characters
WHERE first_name LIKE 'H%' AND LENGTH(first_name) = 5       -- Имя начинается с H и состоит из 5 букв
   OR first_name LIKE 'L%';                                 -- Или начинается с L

SELECT * FROM characters                                    -- Персонажи в возрасте от 50 до 100 лет
WHERE age BETWEEN 50 AND 100; 

SELECT * FROM characters                                    -- Пример использования оператора IN
WHERE last_name IN ('Crabbe', 'Granger', 'Diggory'); 
```

## Агрегация и группировка

```sql
SELECT COUNT(*) FROM characters;                            -- Подсчитать количество персонажей
SELECT AVG(age) FROM characters;                            -- Средний возраст
SELECT faculty, COUNT(*) FROM characters GROUP BY faculty;  -- Количество персонажей по факультетам

SELECT faculty, COUNT(*) FROM characters                    -- Использование HAVING для фильтрации групп
GROUP BY faculty HAVING COUNT(*) > 1;                       
```

## Определение и управление данными

```sql
CREATE TABLE wizards (                                      -- Создать новую таблицу
  id INT PRIMARY KEY,
  name VARCHAR(50),
  house VARCHAR(20)
);                                                          

ALTER TABLE characters ADD birthday DATE;                   -- Добавить новый столбец
ALTER TABLE characters DROP COLUMN birthday;                -- Удалить столбец
DROP TABLE wizards;                                         -- Удалить таблицу целиком
```

## Изменение данных

```sql
DELETE FROM characters WHERE id = 11;                       -- Удалить персонажа с ID 11
UPDATE characters SET age = age + 1 WHERE age IS NOT NULL;  -- Увеличить возраст на 1
```

## Объединение таблиц

```sql
SELECT c.first_name, l.title                                -- Объединить таблицы characters и library
FROM characters c
JOIN library l ON c.id = l.character_id;                    
```

## 🎁 Бонус

Рекомендую ознакомиться с отличной [SQL шпаргалкой](https://www.sqltutorial.org/wp-content/uploads/2016/04/SQL-cheat-sheet.pdf) — пригодится и в ручном, и в автоматизированном тестировании.