# Домашнее задание #8: SQL — Основы работы с базой данных

В [entities.md](entities.md) описание сущностей итогового проекта и ответы на вопросы ДЗ.

## Задание

### SELECT version();

![SELECT version](screenshots/select-version.png)

### Создание таблиц (`01_create_table.sql`)

![Create table](screenshots/create-table.png)

### Описание созданных таблиц

![Describe tables](screenshots/describe-table.png)

### Добавление данных (`02_insert.sql`)

![Insert data](screenshots/insert.png)

### Результаты SELECT-запросов (`03_select.sql`)

![Insert data](screenshots/select.png)

## Запросы в БД

### Получить все записи из таблицы `categories`:

```sql
SELECT * FROM categories;
```

![Select categories](screenshots/select-1.png)

### Вывести товары (название, цена, наличие, категория) в наличии и ценой больше 5000, сортировка по возрастанию цены:

```sql
SELECT
    p.name AS product_name,
    p.price,
    p.in_stock,
    c.name AS category_name
FROM products p
JOIN categories c ON p.category_id = c.id
WHERE p.price > 5000 AND p.in_stock = TRUE
ORDER BY p.price ASC;
```

![Select products](screenshots/select-2.png)

### Вывести 10 пользователей с наибольшей суммой завершенных заказов:

```sql
SELECT
    u.username,
    SUM(o.total_price) AS total
FROM orders o
JOIN users u ON o.user_id = u.id
WHERE o.status = 'completed'
GROUP BY u.id
ORDER BY total DESC
LIMIT 10;
```

![Select users](screenshots/select-3.png)
