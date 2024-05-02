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


