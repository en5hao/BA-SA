# SQL-запросы для анализа библиотечной базы данных

## Задание 1: Найти 5 самых популярных авторов (по количеству выданных книг)

## Задание 2: Найти читателей, взявших > 3 книг в этом месяце (используя GROUP BY и HAVING)

**SQL-запросы:**

```sql
-- ЗАДАНИЕ 1:
SELECT 
    a.author_id,
    COUNT(br.book_id) AS borrow_count
FROM Authors AS a
LEFT JOIN Book_authors AS ba ON a.author_id = ba.author_id
LEFT JOIN Borrows AS br ON ba.book_id = br.book_id
GROUP BY a.author_id
ORDER BY COUNT(br.book_id) DESC
LIMIT 5;

-- ЗАДАНИЕ 2:
SELECT 
    r.reader_id
FROM Readers AS r
LEFT JOIN Borrows AS br ON r.reader_id = br.reader_id
WHERE EXTRACT(MONTH FROM CAST(br.borrow_date AS DATE)) = 5
GROUP BY r.reader_id
HAVING COUNT(br.book_id) > 3;
