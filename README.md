# 📌 SQL

**SQL** (Structured Query Language) is a standard language for managing and manipulating relational databases. It allows QA engineers to retrieve test data, validate changes after actions in the application, and ensure data consistency after different operations — making it a critical tool in manual and automated testing.

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