Question Structure
==================

We created a question file where all the questions are going to be stored, these questions are going to be 
used during the quiz.

.. code::

  {
  "quiz-one": {
    "quiz-title": "General Knowledge",
    "questions": 

The use of ``quiz-one`` is assigned to quiz-one as ``General Knowledge`` where when a user has selected the category 
they will be assigned to the general knowledge category. After the assigning stage we then have the questions 
where the question are wirtten out like this.

.. code::

  {
        "question_title": "What data type is used to store non-whole numbers?",
        "options": ["Integer", "Float", "Boolean", "String"],
        "correct_ans": 1
      },

This structure starts off with ``question_title`` where the user and other users that are in the room can see what the 
question is, then we have the ``options`` where we have 4 different options to choose from, they will be 4 different boxes 
with 4 different answers assigned as seen as ``["Integer", "Float", "Boolean", "String"],`` the users in the room can see the 
4 different answers and then they have to choose which one is the correct answer. Finally we have the ``correct_ans``
which give a value of ``0`` meaning that whatever the users have chosen will depend on what the systems assigned ``correct_ans``
is.

Mathematics
-----------

.. code::

  "quiz-two": {
    "quiz-title": "Mathematics",
    "questions":

This is similar to the first quiz, but here we have quiz 2 where before creating a room they can choose quiz 2 which is assigned as
``quiz-title: Mathematics`` So to access this we click on the drop down menu and we can see the Mathematics section that will give maths 
based questions to the users that are in the same room as the user who created the room.


.. code::

  {
        "question_title": "What is the formula to calculate the area of a circle?",
        "options": ["πr", "πr^2", "2πr", "2πr^2"],
        "correct_ans": 1
      },


Here is pretty much the same example as the first quiz but they are different questions and different answers 
and also in a different section, so the users will get maths based questions and answers.
the ``question_title:`` wil give the users the question and the ``options`` will be what the users can see and click on 
to give in their answers. Then when the user has clicked on the answer, we have the ``correct_ans`` where it will be assigned to the given answers
and see if the user has clicked on the right or wrong asnwer.

The code will repeat the same for all different modules but have different titles and different questions and answers.
So the 3rd and 4th quiz will be named ``Core Computing Concepts`` with questions and answers from that module, and then the 
4th quiz which is ``Networks`` Will have different questions and answers but related to that specific module.