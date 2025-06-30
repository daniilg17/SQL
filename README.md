# 📌 SQL

**SQL** (Structured Query Language) is a standard language for managing and manipulating relational databases. It allows QA engineers to retrieve test data, validate changes after actions in the application, and ensure data consistency after different operations — making it a critical tool in manual and automated testing.

### 📚 Database Tables Description

#### This project works with two main tables in a [Hogwarts-themed database](https://drive.google.com/drive/u/3/folders/1MC0AttnmlAmugifFlX3hG6pssYZDqpPB):

### Table: `characters`

Stores information about characters, including their names, ages, faculty affiliation, patronus, and unique ID.

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

Contains records of books taken by characters, including the issue date, return date, and shelf location.

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

## Basic Queries

```sql
SELECT * FROM characters;                                   -- Select all data from the characters table
SELECT first_name, last_name FROM characters;               -- Select only specific columns
SELECT DISTINCT faculty FROM characters;                    -- Get unique values

SELECT first_name AS "Half-Blood Prince"                    -- Alias example
FROM characters WHERE id = 7; 
```

## Filtering and Sorting

```sql
SELECT * FROM characters WHERE age > 30;                    -- Filter characters older than 30
SELECT * FROM characters WHERE last_name LIKE '%a%';        -- Last names that contain 'a'
SELECT * FROM characters ORDER BY age DESC;                 -- Sort characters by age (descending)

SELECT * FROM characters
WHERE first_name LIKE 'H%' AND LENGTH(first_name) = 5       -- Name starts with H and is 5 letters long
   OR first_name LIKE 'L%';                                 -- OR starts with L

SELECT * FROM characters                                    -- Characters aged between 50–100
WHERE age BETWEEN 50 AND 100; 

SELECT * FROM characters                                    -- IN operator
WHERE last_name IN ('Crabbe', 'Granger', 'Diggory'); 
```

## Aggregations and Grouping

```sql
SELECT COUNT(*) FROM characters;                            -- Count all characters
SELECT AVG(age) FROM characters;                            -- Average age
SELECT faculty, COUNT(*) FROM characters GROUP BY faculty;  -- Count per faculty

SELECT faculty, COUNT(*) FROM characters                    -- Filter groups using HAVING
GROUP BY faculty HAVING COUNT(*) > 1;                       
```                                                        

## Data Definition and Control

```sql
CREATE TABLE wizards (                                      -- Create new table
  id INT PRIMARY KEY,
  name VARCHAR(50),
  house VARCHAR(20)
);                                                          

ALTER TABLE characters ADD birthday DATE;                   -- Add new column
ALTER TABLE characters DROP COLUMN birthday;                -- Remove column
DROP TABLE wizards;                                         -- Drop entire table
```

## Modifying Data

```sql
DELETE FROM characters WHERE id = 11;                       -- Delete character with ID 11
UPDATE characters SET age = age + 1 WHERE age IS NOT NULL;  -- Increase age by 1
```

## Joins and Relationships

```sql
SELECT c.first_name, l.title                                -- Join characters with library books
FROM characters c
JOIN library l ON c.id = l.character_id;                    
```

##  Bonus

You can also check out some great [SQL Cheat Sheets](https://www.sqltutorial.org/wp-content/uploads/2016/04/SQL-cheat-sheet.pdf)