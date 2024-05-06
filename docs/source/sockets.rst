Sockets
=======


Generating rooms
----------------

We made a generate room function so that we can get the ID of that room for the user creating the room,
once that ID has been created, the ID will be displayed on the show rooms where other users can either
look at available rooms or join through RoomID.

How we do this is:

.. code::

  export function generateRoomId() {
  let roomId = Math.floor(Math.random() * 900000) + 100000;
  while (activeRooms.has(roomId)) {
    roomId = Math.floor(Math.random() * 900000) + 100000;
  }
  return roomId.toString();
  }

This function ``generateRoomID`` is assigned to create a random number and ID so that the rooms are different
if we are wnating to create muiltple room access. ``Math.random`` which generates a random number between the assigned
ranges. Once the room ID has been created we have a function of ``return roomID.toString()`` which will display the 
room ID to the user that created a new room.

Starting a quiz 
---------------

Before we are creating a room we are shown what type of subject we want to pick, there will be a nunber of modules
for the students to choose from and then they can create the room once they have done so.

We create random quetsions depending on what the user picks through this function.

.. code::

  export function startQuiz(io, roomId, questions, selectedQuizTitle) {
  const questionsList = questions[selectedQuizTitle].questions;
  let questionIndex = 0;

Which where the function ``startQuiz`` has different params of ``io, roomId, questions, selectedQuizTitle`` where
when the user clicks on each category we will generate that accordingly. Then we have the 
``questions[selectedQuizTitle].questions`` which takes the quiz title for what the user has chosen. After that we have a ``const sendQuestion``
where it will send the first question randomly for the users to start the quiz.

Getting rooms for other users
-----------------------------

We want to make sure that users have a more comfortable access to using the webpage so that when there is an active room, we can 
implement a ``function getRooms`` where we can show the users if there are anyt active rooms for them to join

.. code::

  export function getRooms(socket) {
  socket.emit('roomsList', Array.from(activeRooms.keys()));
  }

Using the branch ``roomList`` will give a dropdown and show the user of an active rooms that are available 
if there are any active rooms then the ``activeRooms.keys`` will display so that the user can use the ID to 
join the room.


Joining rooms
-------------

Now that we have the roomsID and how to start a quiz, we want to make sure that other users can actually join 
the room, we do so by using ``function joinRoom``

.. code::

  export function joinRoom(socket, roomId, io, username) {

  if (roomMembers[roomId] === undefined && activeRooms.has(roomId)) {
    roomMembers[roomId] = { users: [] };
  }

Through this function we want to make sure if there are any activeRooms, we do so by using ``activeRooms.has(roomID)``
this checks if the room has a valid ID and if the room has an invalid ID it gives a room ID error
we use the ``if`` statement to check ``activeRooms.has(roomID) === false`` which then does a 
``socket.emit('roomError')`` not allowing the user to join as it doesn't have an active room ID


Deleting rooms
--------------

We can create rooms, joins room now we want to make it so that the user is also allowed to delete rooms.
We can do this by create a function ``deleteRoom``.

.. code::

  if (roomId && activeRooms.has(roomId)) {
    activeRooms.delete(roomId);
    // console.log(`Room ${roomId} has been deleted`);
    io.emit('roomDeleted', roomId);
  }

The system is looking through the current ID's of the room through ``roomID && activeRooms.has(roomID)``
if the room has both matching then we have a command ``activeRooms.delete(roomID)`` where the room is 
being deleted through the matching ID's.


Sending Messages Between users
------------------------------

.. code::

  export function sendMessage(socket, io, roomId, messageContent, username) {
  if (activeRooms.has(roomId)) {
    messageContent = filter.clean(messageContent);
    io.to(roomId).emit('message', username, messageContent);
  } else {
    socket.emit('roomError', 'Invalid Room ID');
    // console.log('Invalid Room ID provided by user');
  }
}

What is a room if you are not able to communicate through to each other, so we created a ``function sendMessage``
where we check ``if (activeROoms.has(roomId))`` then if the room is active the user have a box where the text is sent, 
then the ``io.to(roomId).emit('message', username, messageContent)`` this check the message that is being sent, then the 
user that is sending the message and the content that the message is which will be displayed for the other users within 
the active room.
