GROUP BY
~~~~~~~~

With some aggregate functions in our tool belt, we’re ready to take
advantage of one of SQL’s more powerful features: GROUP BY. The GROUP BY
statement is used in conjunction with aggregate functions to group the
results by a given column. Doing so allows us to write queries that
return counts, sums, averages, minimums and maximums per group.

So, what is the total amount of contributions per state:

::

   <code>SELECT state, SUM(amount) FROM contributors GROUP BY state;</code>

|image25|

It’s also possible to group by a combination of columns. So, we can get
totals by city and state, as well:

::

   <code>SELECT city, state, SUM(amount) FROM contributors GROUP BY city, state;</code>

|image26|

And we can use the aggregate function in an ORDER BY statement to sort
the results by total amount:

::

   <code>SELECT city, state, SUM(amount) FROM contributors GROUP BY city, state ORDER BY SUM(amount) DESC;</code>

|image27|

The syntax of this last statement is a little tricky. The columns to
group by are separated by commas, but there is no comma before ORDER BY
or DESC.

Most relational database management systems require that every
non-aggregate field in the SELECT statement also be included in the
GROUP BY statement. Because SUM (amount) is an aggregate, we can include
it in the SELECT statement, even though it isn’t included in the GROUP
BY list. But if we want to include city in the SELECT, we generally need
to include it in the GROUP BY as well.

SQLite doesn’t enforce this standard SQL restriction, which in some
cases makes writing the query much simpler but in most cases can lead to
unexpected results. Here’s what happens when we leave the city column
out of the GROUP BY but include it in the SELECT:

|image28|

That’s not at all what we wanted. We’re getting only one row per state
(because we only grouped by state), and we’re getting an apparently
arbitrary city name for each state. (It’s actually the city name from
the row with the highest id, but that’s no help.) So, there’s a good
reason for the standard SQL restriction against this kind of query. If
you’re certain that there is a unique relationship between the column
for SELECT and the columns in the GROUP BY (for example, if we were
grouping by zip and wanted to display the state in the results and we
were certain that there was only one state per zip), then SQLite’s
flouting of this restriction can be seen as a feature and not a bug. But
as a general practice and to make your queries portable to other
systems, you should always include all columns for the SELECT in the
GROUP BY list. If including that column in the GROUP BY isn’t possible,
then you’ll probably need to use a subquery to create the desired
result.

.. |image25| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/amount_by_state.png
.. |image26| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/amount_by_city_state.png
.. |image27| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/city_state_by_amount_desc.png
.. |image28| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/group_by_without_city.png

