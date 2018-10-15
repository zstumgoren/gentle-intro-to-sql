Pick One: Using BETWEEN and IN (NOT IN)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Often you'll want to get a value from within a range. The ``BETWEEN``
operator can do exactly that. Let's see which of our contributors has
given between 500 and 1000 dollars:

::

   SELECT * FROM contributors WHERE amount BETWEEN 500 AND 1000;


|between|

  Note: This query returns the same results as
  ``SELECT * FROM contributors WHERE amount >= 500 AND amount <= 1000;`` — but it's much
  more readable.

At other times, you may need to match values from within a set of
choices. This is where the IN operator comes in handy. Let’s find all
contributors from a few southern states:

::

   SELECT * FROM contributors WHERE state IN ('AL', 'GA', 'FL');


The choices are surrounded by parentheses and separated by commas. And
don’t forget the quote marks around literal strings. here’s the
result:

|in|

  Again, you could have used a compound statement with ``state = 'AL' OR
  state = 'GA' OR state = 'FL'`` to achieve the same result, but the ``IN``
  syntax makes things much clearer, and it's easier to write.

You can also use ``NOT IN`` to find results where a value is not included in
the given set:

::

   SELECT * FROM contributors WHERE state NOT IN ('CA', 'OR', 'AZ');

But beware that ``NOT IN`` won't work with null fields. So, if one of the
rows has a null value for state, it would not be returned by the query
above.

.. |between| image:: ../_static/part2/between.png
.. |in| image:: ../_static/part2/in.png

