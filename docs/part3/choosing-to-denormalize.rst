Why be normal? Denormalization as an informed choice.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Looking at the candidates table, there is another column showing some
repetition: party. Many database designers would extract this column
into its own table and then include a *party_id* foreign key in the
candidates table. It might be a good idea here to use that id rather
than a text field; as it stands, if the data came in with "R,"
"Republican" and "GOP" all appearing in that column, we would have a
real mess. If we had a **parties** table that included only "R," "D" and
"I" (for independent), then we'd know we have a nonstandard value coming in when we tried
to look up the *party_id* for "GOP," for example.

But normalization comes with a cost. Adding that parties table would
mean that, any time we want to show candidate name and party, we'd have
to do a join. And if we wanted contributor, candidate, and party, we’d
have a query with two joins:

::

   SELECT contributors.last_name,
          candidates.last_name,
          parties.name
   FROM contributors
   JOIN candidates ON contributors.candidate_id = candidates.id
   JOIN parties ON candidates.party_id = parties.id;

Doing multiple joins can become rather expensive in terms of memory, so
often developers will create summary tables from the output of a SELECT:

::

   CREATE TABLE contributors_candidates AS
      SELECT contributors.last_name,
             candidates.last_name,
             parties.name
      FROM contributors
      JOIN candidates ON contributors.candidate_id = candidates.id
      JOIN parties ON candidates.party_id = parties.id;

But any changes to the **contributors** or **candidates** tables would
immediately make this summary table out of date, so you'd have to create
a way to update the summary table with each change.

There is another approach: **denormalization**. That is, collapsing your
normalized data into a single table. If you’re interested, check out the
blog post on
`codinghorror <http://www.codinghorror.com/blog/2008/07/maybe-normalizing-isnt-normal.html>`__
and the spirited debate in the comments. I’ll give Jeff Atwood the final
comment here: “As the old adage goes, normalize until it hurts,
denormalize until it works.”

.. |image12| image:: https://github.com/tthibo/SQL-Tutorial/raw/master/tutorial_files/images/multiple_joins.png
