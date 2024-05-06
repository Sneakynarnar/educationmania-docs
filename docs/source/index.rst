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

We use the following ``function login(username, password)`` where we can then use the ``await`` to see if the username and the password is the one matching in the database,
to get the username and the password we use ``SELECT * FROM Accounts WHERE accountName = ? AND accountPassword = ?`` so that when the user name and password is typed
the system will check the database for the correct input, if not then it will output ``Incorrect username or Password.``

:kbd:`Login`

Registering a new account 
-------------------------

Next step was to create a new account / register an account
.. code::

   @param {string} username 
   @param {string} password 
   @returns {Promise<boolean>}

Now we want to register a new user account so we use the same await command so that the database can get the following command
``SELECT * FROM Accounts WHERE accountName = ?, [username]`` so this will check the username that the user has inputted and use that to check the database
if the username does already exist then we use the if function to check else ``if (existingUser)  return "UserAlreadyExists" `` so that we dont have duplicate usernames
if there are duplicate usernames then the friend system will cause an issue as there is more than 1 userID that are the same.
If the username isn't a duplicate then we have the ``await db.run`` which will ``INSERT INTO Accounts`` which is a command to insert a new user into the database under the 
Accounts table with new values and to register that this user is not new and it will assign when the user has joined as a new user.

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

Sending friend request is a huge addon to the page as the users interacting want to see who is online and are able to send and remove friends from their friends list
so we created a ``function sendFriendRequest`` where we check for usernames wiuthin the database. ``if (username === reqeustee)`` then it will ``return "Cannot add self"`` so we check
that the user is not adding them selves as this wont be possible.
We check existing friends, so ``if (existingFriends)`` then it will ``return "User and requestee are already friends"`` not allowing duplicate friend requests

And finally we check if the actual requestee exists, we can't have a user send a random username a request, so we create a if statement
.. code::
   if (!user || !requesteeExists) {
   return 'User does not exist';
   }
   await db.run(
   'INSERT INTO FriendRequests (user, requestee) VALUES (?, ?)', [username, requestee],
   );
   server.notifyFriendRequest(null, user, requestee);
   return 'Success';

We check the if statement if the user actually exists with a return of ``User does not exist`` if when we check through the database with ``await db.run`` and ``INSERT`` function
to check in the database if the user exists, if not then the output will return and error, if the user does exists then the 
``server.notifyFriendRequest`` will give a success message as the ``username`` that was inputted has matched with the one in the database.

:kbd:`Send Friend Request`


Accepting friend Requests
-------------------------

.. code::

   @param {string} username 
   @param {string} requestee 
   @returns {Promise<string>} 

We can send requests to users to send them a friend request but we also need to be able to accept a friend request so we create a function called
``function acceptFriendRequest(username, requestee)`` where in this function we check for ``existingFriendRequests`` we check that through using
``await db.get`` and then select from the friend requests and the requestee.

We then use the ``if (!existingFriendRequests)`` statement to check for a user, if there is nothing then we get ``return "No friend Request from that user"``
and then see if the user exists by typing their name in and adding them, where the database will search for that user,


:kbd:`Accept Friend Request`

Retrieving a friend request for a given username
------------------------------------------------

.. code::

   @param {string} username 
   @returns {Promise<array<Objects>>} 

We want to know if we have recieved a friend request from a user so we created a ``function getFriendRequests(username)`` to check if we have recieved a friend 
request from a user. If not then we can use the ``await db.all`` where we ``SELECT * FROM FriendRequests WHERE requestee = ?, [username]`` to select a username and 
get the username to see if the user has recieved a friend request from a specific user.

Retrieving the friends of a user from the database
--------------------------------------------------

.. code::
   
   @param {Object} res 
   @param {string} username 
   @returns {Array<string>} 

Now that we have a couple users in the database and a friends system, we can check an users friends within the database. 
we crate a ``function getFriends(username)`` to use ``await db.all`` to select a user and then another user from a database.
then we can check if the user is friends with that person within the database. We use the ``for (const friend of friendsRows)`` loop to check for friends and if they are 
on each others friends list, then the ``if (friend.user1 === username)`` statement wants to use the push function ``friends.push(friend.user2)`` where if the friend is on
a users friends list then it checks out if not then it would att the friend to the end off an array.

Ignoring a Friend Request
-------------------------

.. code::

   
   @param {Response} res 
   @param {string} username 
   @param {string} requestee 
   @returns {Promise<string>} 

If we can accept a friend request then we also must ignore a friend request, so we create a ``function ignoreFriendRequest`` so that the user
is able to ignore the incoming friend request. We check the request through the database through a ``SELECT`` query in the database, 
if the user does not exist then it will ``return "No friend request from that user"`` meaning that the user has not sent you a friend request
then we use the ``await db.run`` where if the user does exist then we can ignore it by using the ``DELETE`` query, if it is successfull
we get a ``return "Success"``. 

Removing a Friend from the database
-----------------------------------

.. code::

   @param {string} username 
   @param {string} friend 
   @returns {Promise<string>} 

We can add a friend so we also need to implement a remove a friend system we do this by creating a ``function removeFriend(username, friend)``
to check if that it is the correct username and if they are on the users friends list. We use the ``const existingFriend`= await db.get`` to get the database to ``SELECT`` 
from the database and see if the username does exist and if the they are friends with the user.
We use an ``if (!existingFriend)`` statement to check if the friend exists in the database and in the users friends list, if not then it ``returns "No friend found"``
but if the friend does exist then we use the ``await db.run`` to run a ``DELETE`` query to check username and if they are on the users friends list then it will ``return "Success""``.

Retrieving the Leaderboard
--------------------------


.. code::
   
   @returns {Promise<Array<Objects>>}

Finally we have the database that displays on the leaderboard, to see the users and the different scores, we do this by 
doing ``function getLeaderboard()`` which retrives the leaderbvoard from the database of all the users and then to display the leaderboard nicely, 
we want to create a query with ``await db.all`` that calls a ``SELECT`` query with the totalCorrectAnswers and shows them on the Leaderboard
with the user that has the most correct answers will be on the top of the leaderboard, to display this we call a ``return leaderboard`` statement.



Check how to install through :doc:`usage`


.. toctree::
   :maxdepth: 6

   usage
   setup
   index
   sockets
   quiz
   question