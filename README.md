### notes

- flox pull flox/postgres
- flox edit
```
change into
PGPORT = "5432"
PGUSER = "postgres"
PGPASS = "pgpass"
PGDATABASE = "postgres"
```
- flox activate
- flox services start
- psql
```
postgres=# create database pagila;
CREATE DATABASE

postgres=# \c pagila 
You are now connected to database "pagila" as user "postgres".

pagila=# \i pagila-schema.sql 

pagila=# \q

```

- psql
```
postgres=# \c pagila
You are now connected to database "pagila" as user "postgres".

pagila=# \dt

                    List of relations
 Schema |       Name       |       Type        |  Owner   
--------+------------------+-------------------+----------
 public | actor            | table             | postgres
 public | address          | table             | postgres


pagila=# \q

```

- psql
```
postgres=# \c pagila
You are now connected to database "pagila" as user "postgres".

pagila=# \i pagila-data.sql 

pagila=# \dt
Did not find any relations.

pagila=# \q

```


- psql
```
postgres=# \c pagila
You are now connected to database "pagila" as user "postgres".

pagila=# \dt


                    List of relations
 Schema |       Name       |       Type        |  Owner   
--------+------------------+-------------------+----------
 public | actor            | table             | postgres
 public | address          | table             | postgres
 public | category         | table             | postgres


```

- example queries
```
SELECT
	CONCAT(customer.last_name, ', ', customer.first_name) AS customer,
	address.phone,
	film.title
FROM
	rental
	INNER JOIN customer ON rental.customer_id = customer.customer_id
	INNER JOIN address ON customer.address_id = address.address_id
	INNER JOIN inventory ON rental.inventory_id = inventory.inventory_id
	INNER JOIN film ON inventory.film_id = film.film_id
WHERE
	rental.return_date IS NULL
	AND rental_date < CURRENT_DATE
ORDER BY
	title
LIMIT 5;


    customer    |    phone     |      title       
----------------+--------------+------------------
 OLVERA, DWAYNE | 62127829280  | ACADEMY DINOSAUR
 HUEY, BRANDON  | 99883471275  | ACE GOLDFINGER
 OWENS, CARMEN  | 272234298332 | AFFAIR PREJUDICE
 HANNON, SETH   | 864392582257 | AFRICAN EGG
 COLE, TRACY    | 371490777743 | ALI FOREVER
(5 rows)


```

### Pagila Data
- https://github.com/devrimgunduz/pagila/tree/master