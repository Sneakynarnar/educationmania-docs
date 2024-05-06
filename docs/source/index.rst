Accounts
=========================================




Creating Accounts
-----------------

We have implemented creating accounts where the user is allowed to create an account and view their profile through progression throughout the quiz game

To log into an existing account we used the following code
`If the user name or passowrd is incorrect then we have a promise that resolves to true, false otherwise.`

.. code::

   @param {string} username 
   @param {string} password 
   @returns {Promise<boolean>}

Creating a simple system to where when the user enters their existing username and password the database can
take that information and match it with the users username and password.

if the username and password doesn't match then it would give a login error and for the user to try again.

:kbd:`Login`

Registering a new account 
-------------------------

Next step was to create a new account / register an account
.. code::

   @param {string} username 
   @param {string} password 
   @returns {Promise<boolean>}

We create a register for a new account for the users for non existing users to create a fresh account.
if the credentials from the username in the database seem to match, then an error of ``Username already exists`` will pop up

:kbd:`Create account`


Friend system
-------------

We created a friends system where a user is able to add a friend to their friends list
or remove a friend from their friends list. It is easily accessible from the Homepage or 
their personal profile.

.. code::

   @param {string} username 
   @param {string} requestee 
   @returns {Promise<boolean>} 

The strings for username and requestee is so that we can identify the user sending the friend request and the
user that is receiving the friend request, and then include the promise that resolves to a string indicating 
the result of the opeartion.

:kbd:`Send Friend Request`


Accepting friend Requests
-------------------------

.. code::

   @param {string} username 
   @param {string} requestee 
   @returns {Promise<string>} 

The two strings here represent the username of the user accpeting the friend request and the user who sent
the friend request also the promise string that resolves to a success message if the friend request is accepted
or an error message if no friend request is found. 

:kbd:`Accept Friend Request`

Retrieving a friend request for a given username
------------------------------------------------

.. code::

   @param {string} username 
   @returns {Promise<array<Objects>>} 

This code represents the username for which to recieve the friend request, so that the user that recieves a friend 
request they see that they have recieved it from a specific person, also the promise that resolves to an array of 
friend requests.

Retrieving the friends of a user from the database
--------------------------------------------------

.. code::
   
   @param {Object} res 
   @param {string} username 
   @returns {Array<string>} 

We have a database of all the users that have signed up to Education mania so when dealing with a friends system
we want to be able to retrieve a user from the data base so they can send friend requests or remove them 
from their friends list.

Ignoring a Friend Request
-------------------------

.. code::

   
   @param {Response} res 
   @param {string} username 
   @param {string} requestee 
   @returns {Promise<string>} 

Ignoring a friend request, when an unwanted friend request is sent then the user that is receiving the request can
ignore it, so the database looks at the user that is recieiving the friend request and then the username of the user 
who sent the friend request, then we have a promise that sends a success message if the friend request has been ignored.

Removing a Friend from the database
-----------------------------------

.. code::

   @param {string} username 
   @param {string} friend 
   @returns {Promise<string>} 

We implemented a remove friend system so that when a user has sent a request to the wrong user or doesn't want to keep
the user in their friends list then the user can remove them from their friends list, with a ``param {string} username`` 
which gets the username of the user and a ``param {string} friend`` which will be the username of the friend that will be 
removed and then a ``returns{Promise<string>}`` which sends a success or an error message depending if the user has 
successfully removed them or not.

Retrieving the Leaderboard
--------------------------


.. code::
   
   @returns {Promise<Array<Objects>>}

Finally we have a function of where we can retrieve the leaderboard from the database, this database will look into who has how
many points and display them to the users seeing where they are on the leaderboard
the ``@returns {Promise<Array<Object>>}`` shows the leaderboard array containing account information.



Check how to install through :doc:`usage`


.. toctree::
   :maxdepth: 7

   api
   usage
   setup
   index
   sockets
   quiz