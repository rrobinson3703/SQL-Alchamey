## select database we are working with 
USE sakila;

## Display the first & last names of of all actors 
select first_name, last_name from actor;


SELECT concat(first_name," ", last_name) as Actor_Name
from actor

##select column from table

##2a You need to find the ID number, first name, and last name of an actor, of whom you know only the first name, "Joe.
SELECT 
	first_name, 
    last_name
FROM actor
WHERE
	first_name = "Joe";

#2b. Find all actors whose last name contain the letters GEN
SELECT last_name
FROM actor
WHERE last_name LIKE '%GEN%';

#2c. Find all actors whose last names contain the letters LI. This time, order the rows by last name and first name, in that order:
SELECT last_name, first_name
FROM actor
WHERE last_name LIKE '%LI%';

#2d. Using IN, display the country_id and country columns of the following countries: Afghanistan, Bangladesh, and China:
SELECT country_id, country
FROM country
WHERE country IN ('Afghanistan', 'Bangladesh', 'China')

#3a. You want to keep a description of each actor.
USE sakila;
SELECT * FROM actor;
ALTER TABLE actor
ADD COLUMN middle_name VARCHAR(45);

ALTER TABLE actor
MODIFY middle_name BLOB;

ALTER TABLE actor
DROP COLUMN middle_name;

SELECT * FROM actor

#4a
SELECT last_name, COUNT(last_name) AS "Count of Last Name"
FROM actor
GROUP BY last_name

#4B
SELECT last_name, COUNT(last_name) AS "Count of Last Name"
FROM actor
GROUP BY last_name
HAVING COUNT(last_name) >=2;

# 4c i tried to run the code with just the firstname and it would not go. I needed first and last
UPDATE actor
SET first_name = 'HARPO'
WHERE first_name = 'GROUCHO' AND last_name = 'WILLIAMS';
	
##select column from table
#SELECT first_name, last_name, actor_id
#FROM actor
#WHERE first_name = 'GROUCHO';

#4d Too hasty
 UPDATE actor
 SET first_name = 
 CASE 
 WHEN first_name = 'HARPO' 
 THEN 'GROUCHO'
 ELSE 'MUCHO GROUCHO'
 END
 WHERE actor_id = 172;
 
 #5a. You cannot  the schema of the address table. Which query would you use to re-create it?

SHOW CREATE TABLE address

#6a. Use JOIN to display the first and last names, as well as the address, of each staff member. Use the tables staff and address
SELECT address, first_name, last_name
FROM staff s
INNER JOIN address a ON s.address_id = a.address_id;

#6b staff, payment; join total by staff
SELECT first_name, last_name, SUM(amount)
FROM staff s
INNER JOIN payment p
ON s.staff_id = p.staff_id
GROUP BY s.first_name, s.last_name;

#6c list each film & # of \actors in film_actor and film
SELECT COUNT(actor_id), title
FROM film f
INNER JOIN film_actor fa
ON f.film_id = fa.film_id
GROUP BY title;

#6d how many copies of hunchback impossible
#look in inventory

SELECT COUNT(inventory_id)
FROM film f
INNER JOIN inventory i
ON f.film_id = i.film_id

WHERE title = "Hunchback Impossible";

#6e payment & customers; list sum paid by each customer last name alpha
#How do i put this in alphabetical order. research order by
SELECT SUM(amount), first_name, last_name
FROM payment p
INNER JOIN customer c
ON p.customer_id = c.customer_id
GROUP BY p.customer_id
ORDER BY last_name ASC;

# Subquery title w/letters K&Q &language =English
SELECT title FROM film 
WHERE language_id in
	(SELECT language_id FROM language
	WHERE name = "English")
AND (title LIKE 'K%' OR title LIKE 'Q%');

#7B subquery actors in film Alone Trip
SELECT first_name, last_name
FROM actor
WHERE actor_id IN
(
  SELECT actor_id
  FROM film_actor
  WHERE film_id IN
  (
   SELECT film_id
   FROM film
   WHERE title = 'Alone Trip'
  )
);

#7c email address of customers from Canada. This is a left join 
SELECT country, last_name, first_name, email
FROM country 
LEFT JOIN customer 
ON country.country_id = customer.customer_id
WHERE country = 'Canada';

#7d category family films. I used the Views.
USE sakila;
SELECT title, category
FROM film_list
WHERE category = "Family";

#7e  the most frequently rented movies in descending order.

SELECT title, COUNT(f.film_id) AS "Rental_Count" 
FROM film f
JOIN inventory i
ON (f.film_id= i.film_id)
JOIN rental r
ON (i.inventory_id = r.inventory_id)
GROUP BY title ORDER BY Rental_Count DESC;

#7f
SELECT sum(p.amount), s.store_id
FROM payment p
JOIN staff s
ON (p.staff_id = s.staff_id)
GROUP BY store_id;

#7g. Write a query to display for each store its store ID, city, and country.
SELECT store_id, city, country
FROM store st
JOIN address ad 
ON (st.address_id = ad.address_id)
JOIN city cit
ON (ad.city_id = cit.city_id)
JOIN country co
ON (cit.country_id = co.country_id);

#7H. Write a query to display for each store its store ID, city, and country.
SELECT c.name AS "Top 5", SUM(p.amount) AS "Gross" 
FROM category c
JOIN film_category fc
ON (c.category_id=fc.category_id)
JOIN inventory i 
ON (fc.film_id=i.film_id)
JOIN rental r 
ON (i.inventory_id=r.inventory_id)
JOIN payment p 
ON (r.rental_id=p.rental_id)
GROUP BY c.name ORDER BY Gross  LIMIT 5;

#8a

CREATE VIEW top_five_grossing_genres AS

SELECT name, SUM(p.amount)
FROM category c
JOIN film_category fc
JOIN inventory i
ON i.film_id = fc.film_id
JOIN rental r
ON r.inventory_id = i.inventory_id
JOIN payment p
GROUP BY name
LIMIT 5;



#8b
SELECT * FROM Top_Five_Genres;

#8
DROP VIEW Top_Five_Genres;
