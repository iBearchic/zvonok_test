**Задача 2.1**
Даны две таблицы в PostgresSQL - таблица статей и таблица комментариев к этим статьям

Необходимо написать запрос, который выведет все статьи без комментариев (у которых нет комментариев)
Таблицы тут: http://sqlfiddle.com/#!17/84c62 

**Решение:**
Так как две таблицы маленькие, мой ответ по запросу представлен:
SELECT a.*
FROM article a
LEFT JOIN comment c ON a.id = c.article_id
WHERE c.id IS NULL;

**P.S:**
Если таблица с комментариями (comment) была бы достаточно большой по наполнению, можно было бы посравнивать запрос выше с идей ANTI JOIN ниже:
SELECT a.*
FROM article a
WHERE NOT EXISTS (
    SELECT 1
    FROM comment c
    WHERE c.article_id = a.id
);

Отчет из EXPLAIN ANALYZE показывает схожесть оптимальности запросов при прочих равных
