Nothing can come of nothing: Using IS NULL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Let’s take a look back at our original CREATE statement for the
contributors table:

::

   CREATE  TABLE "main"."contributors" ("id" INTEGER PRIMARY KEY  AUTOINCREMENT  NOT NULL , "last_name" VARCHAR, "first_name" VARCHAR, "city" VARCHAR, "state" VARCHAR, "zip" VARCHAR, "amount" INTEGER);

| 
| Notice that we defined the id column as NOT NULL, which meant that it
  was a required field. Because that field is serving as our unique
  identifier or PRIMARY KEY for the row, it can’t be empty.

The keyword NULL is a special value in SQL. It’s a placeholder for an
empty field. If a field is NULL, it’s really empty. That means it’s not
0. It’s not an empty string (). If you’re of a philosophical mind, you
might call NULL the “nothing that is”. If you’re of a pragmatic mind,
you might just think of it as a placeholder where no value has been
entered.

But being nothing (or a placeholder for on empty value) comes with a
cost. NULL can’t be compared with other data types such as strings. And
we can’t use normal operators to match it, either. So =, <> and friends
don’t work with NULL. Don’t believe me? Try it out:

::

   SELECT * FROM contributors WHERE last_name = NULL;

Instead, to query for null values, we use the keywords IS NULL:

::

   SELECT * FROM contributors WHERE last_name IS NULL;

| 
| |image2|

NULL’s refusal to respond to normal operators can lead to some
unforeseen effects. Take a look at this query, and guess what it should
return:

::

   SELECT * FROM contributors WHERE state = 'VA' AND last_name <> 'Lewis';

 (Remember that <> means the same thing that != does: “is not equal.”)

There are three contributors from VA in the table, Robert Albrecht,
Donald S. Lewis, and someone from Rocky Mount whose name fields are
empty. (Yes, the data did come in like this from the FEC.) You can see
the list by using “Browse & Search” or by running this query: SELECT \*
FROM contributors WHERE state = ‘VA’;.

So, the clause WHERE state = ‘VA’ AND last_name <> Lewis looks like it’s
asking for all contributors from Virginia whose last name is not Lewis.
And it looks like it should return both Albrecht and the Rocky Mount
contributor. But when we run it (cue “Price Is Right” sad horn sound),
we only get Albrecht:

|image3|

“Curiouser and curiouser,” you might say. This makes strict logical
sense when we consider that the NULL data type can’t be compared with
any other data type, but really it does seem a bit of a pain (even to
some of the SQL gurus). The solution is to use IS NULL. Here’s one way
to write the query to get the results we intended:

::

   SELECT * FROM contributors WHERE state = 'VA' AND (last_name <> 'Lewis' OR last_name IS NULL);

(The parentheses are optional here, but they do help express our
intentions.)

And now we get the two expected result rows:

|image4|

IS NOT NULL
^^^^^^^^^^^

The opposite of IS NULL is (drumroll) . . . IS NOT NULL. And it works
pretty much as we’d expect:

::

   SELECT * FROM contributors WHERE state = 'VA' AND last_name IS NOT NULL;

|image5|

This negative form is pretty handy for filtering null values from the
results set.



.. |image2| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/last_name_NULL.png
.. |image3| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/not_lewis.png
.. |image4| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/lewis_or_null.png
.. |image5| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/is_not_null.png

