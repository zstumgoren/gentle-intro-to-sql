
Hello SQL!
~~~~~~~~~~

SQL or Structured Query language is the language used to communicate
with relational databases. What are relational databases? Well, most of
the popular database systems you may know, such as MS Access, MySQL or
SQLite, are all relational. That is, they all use a relational model,
which, it turns out, can be described much like a spreadsheet:

-  Data are organized into tables (relations) that represent a
   collection of similar objects (e.g. contributors).
-  The columns of the table represent the attributes that members of the
   collection share (last name, home address, amount of contribution).
-  Each row in the table represents an individual member of the
   collection (one contributor).
-  And the values in the row represent the attributes of that individual
   (Smith, 1228 Laurel St., $250).

Much of the power of a relational database lies in the ability to query
these relations, both within a table (give me all contributors who
donated at least $500 and who live in Wyoming) and among tables (from
the contributors, judges and litigants tables, give me all contributors
who donated at least $1000 to Judge Crawford and who also had legal
cases over which Judge Crawford presided). SQL is the powerful and
rather minimalist language we use to ask such questions of our data in a
relational database. How minimalist is SQL? The basic vocabulary for
querying data comes down to a few main verbs:

::

   SELECT
   INSERT
   UPDATE
   DELETE

| I imagine you can guess what each of those verbs does, even if you’ve
  never written a database query.
| To create and change the structure of tables in the database, there
  are a few other verbs to use:

::

   CREATE
   DROP
   ALTER

| 
| Those are the keywords that perform almost everything you need to do.
  The language also includes a number of modifiers that help specify the
  action of the verbs, but the core list comes down to a couple dozen
  words. These basic keywords are common across pretty much all
  relational databases. A specific database management system (Access,
  MySQL or SQLite) may add its own extensions to the common keywords,
  but the lion’s share of the work is done with this handful of words,
  and they’re basically the same across database applications.

By combining these simple keywords, you can create remarkably complex
and specific queries. And the basic syntax still reads fairly clearly:

::

   SELECT last_name FROM contributors WHERE state = 'WY';

| 
| The SQL query above reads pretty much like the English sentence for
  the same request:

::

   Select the last name from the contributors table where the contributor's state is WY.

| 
| If you’re using a graphical interface such as a datagrid, that
  interface is simply constructing queries like these behind the scenes.
  So, why not take command of your queries and write them yourself?

A couple of things off the bat:

-  SQL keywords are not case-sensitive. So capitalizing SELECT in the
   statement above is optional. Using all caps for keywords is
   considered good form, though, because it helps distinguish keywords
   from table names or other non-keywords.
-  The statement ends with a semi-colon. This is the standard way of
   ending a statement in SQL. Some systems enforce this convention.

So, let’s dive in. For this tutorial, we will be using SQLite, a free
and open source database manager that’s lightweight and portable.

