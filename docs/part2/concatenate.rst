Pull yourself together: The concatenate operator (\|\|)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sometimes we want to combine values from different columns, either in
the WHERE clause or for the results. SQLite uses the concatenation
operator (\|\|) to combine strings. You can combine both literal strings
(in quotation marks) and column values using this operator.

Say, for instance, we want a nicely formatted list of cities and states
for contributors. To create a single result column that contains the
city and state separated by a comma, we can use this query:

::

   <code>SELECT city || ',' || state FROM contributors ORDER BY state, city;</code>

| 
| We insert the comma and space as a literal string concatenated with
  the values from the city and state columns.

|image14|

Note: Some other database management systems, such as MySQL use the
CONCAT() function to perform concatenation: e.g. SELECT
CONCAT (city, ', ', state) FROM contributors; //WON’T WORK IN SQLITE.

.. |image14| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/concat_city_state.png

