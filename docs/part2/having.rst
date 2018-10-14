HAVING
~~~~~~

Now that we understand grouping and aggregates, let’s try filtering the
results based on an aggregate. To start, let’s find all cities for which
the total contributions is greater than $3,000. Here’s a first stab at
the query:

::

   <code>SELECT city, state, SUM(amount) FROM contributors WHERE SUM(amount) >= 3000  GROUP BY city, state  ORDER BY SUM(amount) DESC;</code>

And . . . no.

|image29|

The error message isn’t exactly friendly, but you can see “misuse of
aggregate: SUM()” if you look closely enough (it also appears in the
“Last Error” field of the SQLite manager once you close the alert box).
Turns out that aggregate functions can’t be used in a WHERE clause. The
WHERE clause acts as a filter on each row in turn, but here we want to
test an expression against a value for a group of rows (SUM (amount)).
The equivalent of a WHERE clause for aggregates is HAVING. It appears
after the GROUP BY:

::

   <code>SELECT city, state, SUM(amount) FROM contributors GROUP BY city, state HAVING SUM(amount) >= 3000 ORDER BY SUM(amount) DESC;</code>

|image30|

To get a better sense of the difference between WHERE and HAVING, let’s
first look at a fairly simple query using WHERE:

::

   <code>SELECT city, state, amount FROM contributors WHERE amount >= 2300;</code>

| 
| This query looks for individual contributors who have given at least
  $2,300, and it returns their city, state and amount.

|image31|

Now let’s make this into an aggregate query by adding a GROUP BY and an
aggregate function:

::

   <code>SELECT city, state, SUM(amount) FROM contributors WHERE amount >= 2300 GROUP BY city, state;</code>

|image32|

We have the same nine cities that we had in the first query (those
cities in which someone donated at least $2,300). But now, rather than
having one row per contributor, we have one row per city. The GROUP BY
eliminates the duplicate entries for cities in which more than one
person contributed at least $2,300. And by using the aggregate function
for SUM (amount), we’re adding up all contributions of at least $2,300
for each city.

Now let’s further filter this list of cities. We want to look only at
cities in which these large contributions ($2,300 or greater) made a big
difference. Let’s call $4000 a big difference, for the sake of argument.
So, we want only those cities for which the total amount of
contributions at this size exceeds $4000. (Looking at the results from
the last query, we know to expect 3 rows, but it’s not always so easy to
see.) Here goes:

::

   <code>SELECT city, state, SUM(amount) FROM contributors WHERE amount >= 2300 GROUP BY city, state HAVING SUM(amount) > 4000;</code>

And bam!

|image33|

.. |image29| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/warning_aggregate_where.png
.. |image30| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/having_amount_greater.png
.. |image31| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/where_gt_2300.png
.. |image32| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/where_gt_2300_with_group.png
.. |image33| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/where_plus_having.png

