Knowing your limitations: Using LIMIT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

So far, all of our queries have returned the full result set of rows
matching the WHERE clause. But sometimes you only want a subset of the
results. Let’s use the LIMIT keyword to get the top 20 contributors by
contribution.

First we order the results by amount (in descending order), and then we
limit the results to only the first 20 rows:

::

   <code>SELECT * FROM CONTRIBUTORS ORDER BY amount DESC LIMIT 20;</code>

|image6|

And if there aren’t enough matching rows to reach the specified limit,
the limit is simply ignored:

::

   <code>SELECT * FROM contributors WHERE amount > 2100 LIMIT 20;</code>


.. |image6| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/top_twenty_contributors.png

