Setting up the database
=======================

Running the database
--------------------

When creating a friend system and making sure people can create accounts we need to make sure that 
we have a database that can store the users credentials in there, so we made a database that can 
do just the job.

.. code::

  await db.run('DROP TABLE IF EXISTS Accounts;');

In this command, we automatically drop the tables if the accounts table exists, reason for this is so 
that we have no errors or duplicate account creations happening. The ``DROP TABLE IF EXISTS Accounts``
does the job of dropping the table under that table name.

We do the same with all the tables that are required within the database.

.. code::

  await db.run('DROP TABLE IF EXISTS Friends');

This looks for a ``Friends`` table and if it has been identified then it will drop that table.

Dropping Table for Friend Requests
----------------------------------

.. code::

  await db.run('DROP TABLE IF EXISTS FriendRequests');

Same with the other explanations, this does the same as the other commands but it has a changed table name,
here we have a table name of ``FriendRequests`` making sure that the database will delete the table that is named
``FriendRequests``