Quiz Functionality
==================

In our QuizMania, we have quizes already setup for students to undertake 
rapid thinking through the quiz with friends, we also have a section where students can add 
their own subject and questions and answers.

we have a function called storeQuiz, where in this function we have a set quiz where it pulls from
the database and sets up the quiz depending on the choice that the students wanted to take the quiz on.


.. code::

  export async function getQuestions() {
  const db = await connect;
  const questions = await db.all('SELECT * FROM Questions');
  return questions;
  }

We create a function that gathers the questions, when the user has selected the quiz they want to take, 
the server will take the questions from the database and portray them for the user to read those question
and answer them accordingly.


.. code::
  export async function getRandomQuestionsFromCategory(count, category) {
  const db = await connect;
  const questions = await db.all('SELECT * FROM Questions WHERE category = ?', [category]);

Now we want to make sure that the questions are randomised, we cant keep the question and answers the same 
as we dont want the user to guess the question constantly, so we randomise the questions and the answers, we get the random 
questions by using ``const randomQuestion = questions[randomIndex];`` to generate us random questions.

.. code::

  @param {number} count 
  @param {string} category
  @returns {Promise<Array<Object>>}


The ``@param {number}`` is the number of random questions to retrieve then the 
``@param {string} category`` is the category of questions that we will retrieve from, depending on what quiz the user wants to choose,
and then the ``@returns{Promise<Array<Object>>}`` where a promise that resolves to an array of random questions.