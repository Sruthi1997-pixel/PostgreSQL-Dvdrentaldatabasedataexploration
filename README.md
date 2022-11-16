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
**
a. Return the customer IDs of customers who have spent at least $110 with the staff member who has an ID of 2.**
SELECT customer_id,sum(amount)
FROM payment
WHERE staff_id=2
GROUP BY customer_id
HAVING sum(amount) > 100;

**b. How many films begin with the letter J?**

SELECT COUNT(*) FROM film WHERE title LIKE 'J%';

**c. What customer has the highest customer ID number whose name starts with an 'E' and has an address ID lower than 500?**

SELECT first_name,last_name,customer_id
FROM customer
WHERE first_name LIKE 'E%' AND address_id < 500
ORDER BY customer_id DESC LIMIT 1;

** INNER JOIN-customer table,payment table (here customer_id is present in both the tables,so I am mentioning it with table name,first_name is unique and is peresent in customer table,so need to mention it by .tablename **

SELECT payment,payment.customer_id,first_name
FROM payment
INNER JOIN customer
ON payment.customer_id=customer.customer_id;

** FULL OUTER JOIN-grabs everything from both the tables,whether there is a match in both the tables or whether info is present only in one table **
SELECT * FROM registrations
FULL OUTER JOIN logins
ON registrations.name=logins.name

***** We have introduced new privacy policy where we do not want customers who have never purchased anything or a payment which is not associated with the customer*****
*** FULL OUTER JOIN with WHERE ***
SELECT * FROM registrations
FULL OUTER JOIN logins
ON registrations.name=logins.name
WHERE registrations.reg_id IS NULL OR
logins.log_id IS NULL

*** FULL OUTER JOIN results in records which are unique to both the tables,there is no match ****

***** How can we get a list of students who scored better than the average grade *******
SELECT grade,student FROM
test_score 
WHERE grade> (SELECT AVG(grade) FROM test_score)

