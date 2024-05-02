Usage
=====

.. _installation:

Installation
------------

To use Education mania we want to first install node. once node has been installed we can run this website with the following command ``npm run dev`` wait for the command to finish, now we can run the webpage and start through Logging in / Signing up


Interacting with Education Mania
----------------

When loading into Education mania, we have a start up page where we can ``create an account`` or ``login`` with an existing account.
When creating an account we want to click on the signup link which redirects you to create your account.
Finally the account creating part is done, we are redirected to the main page where all the fun happens
to start, we have 2 buttons that show, ``start a room`` or ``show available rooms``, we want to click on ``start a room`` where this will generate a code, 
once this code has been generated, we click on it and share it to the people wanting to join the room, or an alternative is to just click on show room which will give the 
available room to join, now that we have gotten to that stage we can start the quiz game from there.


Friend System
--------------

We have a friend system that can allow the user to send each other friend requests or remove them from their profile, this friend system can be managed from the ``profile``
or it can be managed through the ``home page`` on the right.
On the right hand side of the home page we see that there it shows the ``active`` users and ``offline`` users, also below that we can ``Remove/Add friends``. This is a easier approach to 
accessing friends and seeing who is online to play with.














To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

