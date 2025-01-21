# Music Store SQL Project

**Database and Tools**
- PostgreSQL
- PG admin

**Key Highlights**

## Objectives:

- Identify the senior-most employee based on job title.
- Determine top-performing countries, cities, and customers based on revenue.
- Analyze music preferences to uncover popular genres and artists.

**Challenges Solved:**

- Ranked cities and customers by revenue for event planning and promotions.
- Identified rock music listeners and invited top artists for potential partnerships.
- Calculated revenue contribution by customers for individual artists.

**Advanced Insights:**

- Found the most popular music genre in each country by analyzing purchase patterns.
- Identified the top-spending customers for each country, even accounting for ties.

**SQL Techniques Used:**

- Joins: For linking multiple tables like customers, invoices, and tracks.
- Aggregations: To calculate sums, averages, and totals for meaningful metrics.
- Subqueries: To solve nested problems like finding average song lengths.
- Ranking Functions: For determining top contributors (e.g., customers, cities).
- Conditional Logic: To handle scenarios with tied results.
- 
**Additional Features:**

- Optimized queries for large datasets to ensure efficient performance.
- Comprehensive comments for better readability and understanding.

**Schema**

![Schema](MusicDatabaseSchema.png)

# SOLUTIONS:

- 1. Who is the senior most employee based on job title?
```sql
SELECT * FROM employee
Order By levels Desc
Limit 1
```

- 2. Which countries have the most Invoices? 
```sql
SELECT billing_country, Count(1) AS Total_invoices
FROM invoice
Group By billing_country
Order By 2 Desc
```

- 3. What are top 3 values of total invoice? 
```sql
SELECT total AS Total_Value
FROM invoice
Order By 1 Desc
Limit 3
```

- 4. Which city has the best customers? We would like to throw a promotional Music Festival in the city we made the most money. Write a query that returns one city that has the highest sum of invoice totals. Return both the city name & sum of all invoice totals.
```sql
SELECT billing_city, SUM(total) AS Invoice_Totals
FROM invoice
GROUP BY 1
Order By 2 Desc
LIMIT 1
```

- 5. Who is the best customer? The customer who has spent the most money will be declared the best customer. Write a query that returns the person who has spent the most money.
```sql
SELECT first_name || ' ' || last_name AS full_name, SUM(total) AS total_spent
FROM customer c
JOIN invoice i ON c.customer_id = i.customer_id
GROUP BY 1
Order By 2 Desc
LIMIT 1
```

- 6. Write query to return the email, first name, last name, & Genre of all Rock Music listeners. Return your list ordered alphabetically by email starting with A 
```sql
SELECT first_name || ' ' || last_name AS C_Name, email, g.name
FROM customer c
JOIN invoice i ON c.customer_id = i.customer_id
JOIN invoice_line il ON il.invoice_id = i.invoice_id
JOIN track t ON il.track_id = t.track_id
JOIN genre g ON t.genre_id = g.genre_id
WHERE g.name like 'Rock'
Order by email 
```

- 2. Let's invite the artists who have written the most rock music in our dataset. Write a query that returns the Artist name and total track count of the top 10 rock bands.
```sql
SELECT art.name, COUNT(g.name)
FROM artist art
JOIN album a ON art.artist_id = a.artist_id
JOIN track t ON a.album_id = t.album_id
JOIN genre g ON t.genre_id = g.genre_id
WHERE g.name = 'Rock'
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10
```










































