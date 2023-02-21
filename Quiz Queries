--Question Set 1:-

--#Question 1: Which countries have the most Invoices?

SELECT BillingCountry, 
	COUNT(InvoiceId) Invoices
FROM Invoice
GROUP by 1
ORDER by 2 DESC;


--#Question 2: Which city has the best customers?

SELECT BillingCity, 
	SUM(Total) total
FROM Invoice
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;


--#Question 3: Who is the best customer?

SELECT c.CustomerId, c.FirstName , c.LastName, 
	SUM(i.Total) total
FROM Invoice i
JOIN Customer c
ON i.CustomerId = c.CustomerId
GROUP by 1
order by 4 DESC
LIMIT 1;


--#Question Set 2:-


/*
#Question 1:
Use your query to return the email, first name, last name,
and Genre of all Rock Music listeners (Rock & Roll would be considered a different category for this exercise)
Return your list ordered alphabetically by email address starting with A.
*/

SELECT DISTINCT c.Email, c.FirstName, c.LastName, g.Name
FROM Customer c
JOIN Invoice i
ON c.CustomerId = i.CustomerId
JOIN InvoiceLine il
ON i.InvoiceId = il.InvoiceId
JOIN Track t
ON t.TrackId = il.TrackId
JOIN Genre g
ON t.GenreId = g.GenreId
WHERE g.Name = 'Rock'
ORDER by 1 ;

--#Question 2: Who is writing the rock music?

SELECT ar.ArtistId, ar.Name, 
	COUNT(al.AlbumId)
FROM Artist ar
JOIN Album al
ON ar.ArtistId = al.ArtistId
JOIN Track t
ON t.AlbumId = al.AlbumId
JOIN Genre g
ON t.GenreId = g.GenreId
WHERE g.Name = 'Rock'
GROUP by 1
ORDER by 3 DESC
LIMIT 10;

/*
#Question 3
1-First, find which artist has earned the most according to the InvoiceLines?
*/

SELECT ar.Name Artist, 
	ROUND(SUM(il.UnitPrice * il.Quantity), 2) as Profit
FROM Artist ar
JOIN Album al
ON ar.ArtistId = al.ArtistId
JOIN Track t
ON t.AlbumId = al.AlbumId
JOIN InvoiceLine il
ON il.TrackId = t.TrackId
GROUP by 1
ORDER by 2 DESC
LIMIT 5;

/*
2-Now use this artist to find which customer spent the most on this artist?
*/

SELECT ar.Name, 
	SUM(il.UnitPrice * il.Quantity) as AmountSpent,
	c.CustomerId, c.FirstName, c.LastName
FROM Artist ar
JOIN Album al
ON ar.ArtistId = al.ArtistId
JOIN Track t
ON t.AlbumId = al.AlbumId
JOIN InvoiceLine il
ON il.TrackId = t.TrackId
JOIN Invoice i
ON i.InvoiceId = il.InvoiceId
JOIN Customer c
ON c.CustomerId = i.CustomerId
GROUP by 1,3
HAVING ar.Name = 'Iron Maiden'
ORDER by 2 DESC;



--#Advanced Questions:-
/*
#Question 1:
We want to find out the most popular music Genre for each country.
We determine the most popular genre as the genre with the highest amount of purchases.
Write a query that returns each country along with the top Genre.
For countries where the maximum number of purchases is shared, return all Genres.
*/

WITH total_amount as (
SELECT  
	SUM(il.Quantity) as amount , 
	BillingCountry as Country, g.Name, g.GenreId
FROM Genre g
JOIN Track t
ON g.GenreId = t.GenreId
JOIN InvoiceLine il
ON il.TrackId = t.TrackId
JOIN Invoice i
ON i.InvoiceId = il.InvoiceId
GROUP by 2,3
),

max_amount as(
   SELECT 
	 MAX(amount) as max_amount, Country
	 FROM total_amount
	 GROUP by 2 
)

SELECT t.amount as Purchases, t.Country, t.Name, t.GenreId
FROM total_amount t
JOIN max_amount m
ON t.Country = m.Country AND t.amount = m.max_amount
ORDER by 2;

/*
#Question 2:
Return all the track names that have a song length longer than the average song length. 
Though you could perform this with two queries.
Imagine you wanted your query to update based on when new data is put in the database.
Therefore, you do not want to hard code the average into your query. 
You only need the Track table to complete this query.
Return the Name and Milliseconds for each track. Order by the song length with the longest songs listed first.
*/

SELECT Name, Milliseconds
FROM Track
WHERE Milliseconds > (SELECT AVG(Milliseconds) FROM Track)
ORDER by 2 DESC;

/*
#Question 3:
Write a query that determines the customer that has spent the most on music for each country.
Write a query that returns the country along with the top customer and how much they spent. 
For countries where the top amount spent is shared, provide all customers who spent this amount.
You should only need to use the Customer and Invoice tables.
*/

WITH total_spent as(
SELECT BillingCountry as Country, 
		SUM(Total) TotalSpent, CustomerId
		FROM Invoice
		GROUP by 1,3
),

max_spent as(
SELECT Country, 
	MAX(TotalSpent) as TotalSpent
FROM total_spent
GROUP by 1)

SELECT t.Country, t.TotalSpent, c.FirstName, c.LastName, t.CustomerId
FROM total_spent t
JOIN max_spent m
ON t.Country = m.Country AND t.TotalSpent = m.TotalSpent
JOIN Customer c
ON c.CustomerId = t.CustomerId
ORDER by 1 DESC;










