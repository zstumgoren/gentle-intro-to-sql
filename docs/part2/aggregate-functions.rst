Aggregate Functions: COUNT, MAX, MIN, SUM, AVG
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Aggregate functions allow us to perform calculations on values across
rows. Using them, we can start to do some pretty interesting data
analysis. To specify a column to use for the aggregate, pass the column
name as the argument in parentheses: e.g. COUNT (counted_column). Here’s
a quick run through some useful aggregate functions:

COUNT()
^^^^^^^

How many contributors do we have from California?

::

   <code>SELECT COUNT(id) FROM contributors WHERE state = 'CA';</code>

|image17|

The COUNT (id) function counts the number of unique ids. We could also
have used COUNT (*), which will count the number of rows. The result
will be the same.

COUNT() can also be used with DISTINCT to return the number of distinct
instances. For example, how many distinct ZIP Codes are there in the
table?

::

   <code>SELECT COUNT(DISTINCT zip)  FROM contributors;</code>

| 
| (Note that the the DISTINCT keyword comes inside the parentheses. It
  is part of the argument passed to COUNT().
| |image18|

MIN() and MAX()
^^^^^^^^^^^^^^^

What is the maximum amount that any of our contributors has given?

::

   <code>SELECT MAX(amount) FROM contributors;</code>

|image19|

SUM()
^^^^^

What is the total amount of contributions from Georgia?

::

   <code>SELECT SUM(amount) FROM contributors WHERE state = 'GA';</code>

|image20|

AVG()
^^^^^

What is the average amount contributed?

::

   <code>SELECT AVG(amount) FROM contributors;</code>

|image21|

(Of course, the usual caveats about using averages apply. I heard a nice
example recently: “Which major at UNC produces graduates with the
highest average salary?” Apparently, it was Geography, Michael Jordan’s
major. Even if it isn’t true, it’s a nice warning about the way outliers
can skew averages.)

.. |image17| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/count_ca.png
.. |image18| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/distinct_zip.png
.. |image19| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/max_amount.png
.. |image20| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/sum_ga.png
.. |image21| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/avg_amt.png

