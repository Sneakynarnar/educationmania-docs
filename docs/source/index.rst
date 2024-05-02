Welcome to Education Manias Documentation
-----------------------------------------



Creating Accounts
-----------------

We have implemented creating accounts where the user is allowed to create an account and view their profile through progression throughout the quiz game

To log into an existing account we used the following code
`If the user name or passowrd is incorrect then we have a promise that resolves to true, false otherwise.`

.. code::

   *Logs in a user with the provided username and password
   @param {string} username - The username of the account.
   @param {string} password - The password of the account
   @returns {Promise<boolean>} - A promise that resolves to true if the login is successful, false otherwise

:kbd:`Login`

Registering a new account 
-------------------------

Next step was to create a new account / register an account
.. code::

   *Registers a new user account
   @param {string} username - The username for the new account.
   @param {string} password - The password for the new account
   @returns {Promise<boolean>} - A promise that resolves to a string indicating the registration status.

:kbd:`Create account`


Friend system
-------------

We created a friends system where a user is able to add a friend to their friends list
or remove a friend from their friends list. It is easily accessible from the Homepage or 
their personal profile.

.. code::

   * Sends a friend request from one user to another
   @param {string} username - The username of the user sending the friend request.
   @param {string} requestee - The username of the user receiving the friend request.
   @returns {Promise<boolean>} - A promise that resolves to a string indicating the result of the opeartion.

:kbd:`Send Friend Request`


Accepting friend Requests
-------------------------

.. code::

   *Accepts a friend request from one user to another.
   @param {string} username - The username of the user accepting the friend request.
   @param {string} requestee - The username of the user who sent the friend request.
   @returns {Promise<string>} - A promise that resolves to a success message if the friend request is accepted, or an error message if no friend request is found

:kbd:`Accept Friend Request`

Retrieving a friend request for a given username
------------------------------------------------

.. code::

   @param {string} username - The username for which to retrieve friend requests.
   @returns {Promise<array<Objects>>} - A promise that resolves to an array of friend requests.

   export async function getFriendRequest(username) {
      const db = await connect;
      const friendRequest = await db.all(
         'SELECT * FROM FriendRequests WHERE requestee = ?', [username],
      );
      return friendRequests;
      }


Retrieving the friends of a user from the database
--------------------------------------------------



.. code::
 * @param {Object} res - The response object.
 * @param {string} username - The username of the user.
 * @returns {Array<string>} - An array of usernames representing the user's friends.
 */
export async function getFriends(username) {
   const db = await connect;
   const friendsRows = await db.all(
    'SELECT * FROM friends WHERE user1 = ? OR user2 = ?', [username, username],
   );
   const friends = [];
   for (const friend of friendsRows) {
      if (friend.user1 === username) {
      friends.push(friend.user2);
   } else {
      friends.push(friend.user1);
   }
}
return friends;
}


Ignoring a Friend Request
-------------------------

.. code::
/**
   Ignores a friend request.

   @param {Response} res - The response object.
   @param {string} username - The username of the user receiving the friend request.
   @param {string} requestee - The username of the user who sent the friend request.
   @returns {Promise<string>} A promise that resolves to a success message if the friend request is ignored, or an error message if no friend request is found.
 */
export async function ignoreFriendRequest(username, requestee) {
   const db = await connect;
   const existingFriendRequests = await db.get(
    'SELECT * FROM FriendRequests WHERE user = ? AND requestee = ?', [username, requestee],
   );
   if (!existingFriendRequests) {
      return 'No friend request from that user';
   }
   await db.run(
      'DELETE FROM FriendRequests WHERE (user = ? AND requestee = ?)', [username, requestee],
   );
   return 'Success';
}


Removing a Friend from the database
-----------------------------------

.. code::

   /**
   Removes a friend from the database.
   @param {string} username - The username of the user.
   @param {string} friend - The username of the friend to be removed.
   @returns {Promise<string>} A promise that resolves to a success message or an error message.
 */
export async function removeFriend(username, friend) {
   const db = await connect;
   const existingFriend = await db.get(
    'SELECT * FROM friends WHERE (user1 = ? AND user2 = ?) OR (user1 = ? AND user2 = ?)',
      [username, friend, friend, username],
   );
   if (!existingFriend) {
      return 'No friend found';
   }
   await db.run(
      'DELETE FROM friends WHERE (user1 = ? AND user2 = ?) OR (user1 = ? AND user2 = ?)',
      [username, friend, friend, username],
   );
   return 'Success';
}