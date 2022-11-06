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

SELECT customer_id,sum(amount)
FROM payment
GROUP BY customer_id
ORDER BY sum(amount) DESC LIMIT 5;

**4.We are launching a platinum service for our most loyal customers.
We will assign platinum status to customers that have had 40 or more transaction payments.
What customer IDs are eligible for platinum status? **

SELECT customer_id,COUNT(payment_id) 
FROM payment
GROUP BY customer_id
HAVING COUNT(payment_id) > 40;

**5.What are the customer IDs of customers who have spent more than $100 in payment transactions with our
staff?**

SELECT customer_id,sum(amount)
FROM payment
WHERE staff_id=2
GROUP BY customer_id
HAVING sum(amount) > 100;

**6.COMPLETE THE FOLLOWING TASKS!

a. Return the customer IDs of customers who have spent at least $110 with the staff member who has an ID of 2.

The answer should be customers 187 and 148.

b. How many films begin with the letter J?

The answer should be 20.

c. What customer has the highest customer ID number whose name starts with an 'E' and has an address ID lower than 500?

The answer is Eddie Tomlin



