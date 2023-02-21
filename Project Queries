/*Question 1:who is the Best Customer?*/
SELECT (c.FirstName || " " || c.LastName) AS Customer, 
	SUM(i.Total) 'Total$'
FROM Invoice i
JOIN Customer c 
ON i.CustomerId = c.CustomerId
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10;


/*Question 2:What are the most Profitable Genres?*/
SELECT g.Name AS Genre,
	ROUND(SUM(il.UnitPrice * il.Quantity), 2) AS Profit
FROM InvoiceLine il
JOIN Track t 
ON t.TrackId = il.TrackId
JOIN Genre g 
ON t.GenreId = g.GenreId
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10;


/* Question 3:What is the Album Length distribution?*/
SELECT al.Title Album, 
	ROUND(SUM(t.Milliseconds)/1000, 2) 'Length(sec)'
FROM Album al
JOIN Track t 
ON al.AlbumId = t.AlbumId
GROUP BY 1
ORDER BY 2 DESC;


/*#Question 4:Who is writing the most Songs?*/
SELECT ar.Name, 
	COUNT(t.TrackId) Songs
FROM Artist ar
JOIN Album al
ON ar.ArtistId = al.ArtistId
JOIN Track t 
ON t.AlbumId = al.AlbumId
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10;
