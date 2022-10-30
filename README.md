# PostgreSQL-Dvdrentaldatabasedataexploration

Description:Exploring the data in DVD Rental Database in PostGreSQL.
Viewing Data in the table:
SELECT * FROM payment;

**1.How many payments did each staff member handle and who gets the bonus?**

SELECT staff_id,count(*)
FROM payment
GROUP BY staff_id
ORDER BY count(amount) DESC; 

**2.What is the average replacement cost per MPAA rating?**

SELECT ROUND(AVG(replacement_cost),2),rating
FROM film
GROUP BY rating;

**3.What are the customer IDs of the top five customers based off total expenditure or total spend?**

