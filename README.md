# API Documentation for endpoints
-----------------------------------------------------------------------------------------------------------

### GET /categories


- General:

Returns all categories

sample: 
```
curl http://localhost:5000/categories
```
```
{
        "categories": {
            "1": "Science", 
            "2": "Art", 
            "3": "Geography", 
            "4": "History", 
            "5": "Entertainment", 
            "6": "Sports"
        }, 
        "success": true
    }
```

### Get /questions

General:

1) Returns questions
2) questions are returned paginated
3) pages can be queried by string

EX: curl http:127.0.0.1:5000/questions
```
{
    "categories": {
        "1": "Science",
        "2": "Art",
        "3": "Geography",
        "4": "History",
        "5": "Entertainment",
        "6": "Sports"
    },
    "questions": [
        {
            "answer": "Tom Cruise",
            "category": 5,
            "difficulty": 4,
            "id": 4,
            "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
        },
        {
            "answer": "Maya Angelou",
            "category": 4,
            "difficulty": 2,
            "id": 5,
            "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
        },
        {
            "answer": "Edward Scissorhands",
            "category": 5,
            "difficulty": 3,
            "id": 6,
            "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
        },
        {
            "answer": "Muhammad Ali",
            "category": 4,
            "difficulty": 1,
            "id": 9,
            "question": "What boxer's original name is Cassius Clay?"
        },
        {
            "answer": "Brazil",
            "category": 6,
            "difficulty": 3,
            "id": 10,
            "question": "Which is the only team to play in every soccer World Cup tournament?"
        },
        {
            "answer": "Uruguay",
            "category": 6,
            "difficulty": 4,
            "id": 11,
            "question": "Which country won the first ever soccer World Cup in 1930?"
        },
        {
            "answer": "George Washington Carver",
            "category": 4,
            "difficulty": 2,
            "id": 12,
            "question": "Who invented Peanut Butter?"
        },
        {
            "answer": "Lake Victoria",
            "category": 3,
            "difficulty": 2,
            "id": 13,
            "question": "What is the largest lake in Africa?"
        },
        {
            "answer": "The Palace of Versailles",
            "category": 3,
            "difficulty": 3,
            "id": 14,
            "question": "In which royal palace would you find the Hall of Mirrors?"
        },
        {
            "answer": "Agra",
            "category": 3,
            "difficulty": 2,
            "id": 15,
            "question": "The Taj Mahal is located in which Indian city?"
        }
    ],
    "success": true,
    "total_questions": 19
}
```

-----------------------------------------------------------------------------------------------------------

### DELETE /questions/int:id\
General:
Deletes questions by ID

Sample: 
```
curl http://127.0.0.1:5000/questions/6 -X DELETE 
```
```
        {
          "success": "True",
          "message": "Question successfully deleted"
        }
```
-----------------------------------------------------------------------------------------------------------


### POST /questions
General:
Creates a new question based on a payload.

Sample: 
```
curl http://127.0.0.1:5000/questions -X POST -H "Content-Type: application/json" -d '{ "question": “Primary sclerosing biliary stenosis is caused primarily by which condition?”, "answer": “auto-immune dysfunction”, "difficulty": 5, "category": “2” }'
```
```
{
  "message": "Question successfully created!",
  "success": true
}
```
-----------------------------------------------------------------------------------------------------------


### POST /questions/search
General:
returns questions that has the search substring

Sample: 
```
curl http://127.0.0.1:5000/questions/search -X POST -H "Content-Type: application/json" -d'{"searchTerm": “Medical”}’ 
```
```
{
  "questions": [
    {
      "answer": “Kartagener’s disease”,
      "category": 2,
      "difficulty": 4,
      "id": 4,
      "question": “Which medical condition causes ciliary stagnation within primarily the respiratory system but also sexual system?”
    }
  ],
  "success": true,
  "total_questions": 20
}
```
-----------------------------------------------------------------------------------------------------------


### GET /categories/int:id\/questions
General:

Gets questions by category using the id from the url parameter.

Sample: 
```
curl http://127.0.0.1:5000/categories/1/questions 

{
  "current_category": "Science",
  "questions": [
    {
      "answer": “three”,
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": “How many columns compose the human penis?”
    },
    {
      "answer": “False”,
      "category": 1,
      "difficulty": 3,
      "id": 21,
      "question": “True or False: UTI is best treated with cyclobenzaprine?”
    },
    {
      "answer": “blood marrow transplant”,
      "category": 1,
      "difficulty": 4,
      "id": 22,
      "question": “What is the most common way for human chimerism to form?”
    }
  ],
  "success": true,
  "total_questions": 3
}


-----------------------------------------------------------------------------------------------------------


### POST /quizzes
General
Takes the category and previous questions in the request.

Return random question not in previous questions.

Sample: 
```
curl http://127.0.0.1:5000/quizzes -X POST -H "Content-Type: application/json" -d '{"previous_questions": [5, 9], "quiz_category": {"type": “history”, "id": "4"}}'
```
```
{
  "question": {
    "answer": "George Washington Carver",
    "category": 4,
    "difficulty": 2,
    "id": 12,
    "question": "Who invented Peanut Butter?"
  },
  "success": true
}
```

-----------------------------------------------------------------------------------------------------------



# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7



1) NODE MODULES HAS BEEN COMPRESSED

2) test_flaskr had 4 errors. There are now zero errors. 
 I sincerely hope I understood what I needed to do here. 

3) My original README was in a different file, I have placed the contents within this 
file. 



















Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior. 

1. Use Flask-CORS to enable cross-domain requests and set response headers. 
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories. 
3. Create an endpoint to handle GET requests for all available categories. 
4. Create an endpoint to DELETE question using a question ID. 
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score. 
6. Create a POST endpoint to get questions based on category. 
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question. 
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions. 
9. Create error handlers for all expected errors including 400, 404, 422 and 500. 

REVIEW_COMMENT
```
Trivia API

This web application allows users to post, delete, and ‘play’ trivia with each other using a webpage. 

You will be able to:

1) display questions and by category.
2) Questions will be able to reveal category and difficulty rating. 
3) Delete questions
4) You can search for questions via a text query
5) Play the game



-----------------------------------------------------------------------------------------------------------



Getting Started:

Install your dependencies

1) Python (3.8.4+)
2) Virtual Environment

Navigate to the /backend folder and run:

pip install -r requirements.txt
or
pip3 install -r requirements.txt

Check to see Werzkreug is up to date. 



-----------------------------------------------------------------------------------------------------------



Key dependencies:

1) FLASK. This is a microframework and allows for requests and responses
2) FLASK-CORS is how we’ll handle cross origin requests from the /frontend
3) SQLAlchemy can work in __init__.py and will allow reference from models.py. 

-----------------------------------------------------------------------------------------------------------


DATABASE:

Run POSTGRES and restore a database using the trivia.psql file included in the form. 
Go to backend and run:

psql trivia_test<trivia.psql



-----------------------------------------------------------------------------------------------------------


RUNNING THE SERVER:

Within /backend folder:

run this is terminal:

export FLASK_APP=flaskr
export FLASK_ENV=development
flask run


-----------------------------------------------------------------------------------------------------------


TESTING:

If you do not have ‘trivia_test’ database created, create one using:

CREATE DATABASE trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py


-----------------------------------------------------------------------------------------------------------


Frontend Dependencies:

Using NPM to manage software dependencies. From the /frontend directory run:

npm install


-----------------------------------------------------------------------------------------------------------


Run FRONTEND in developer mode:

The front-end was created using the CREATE-REACT-APP. To activate it in developer mode, use:

npm start

open Http://localhost:3000 to view it in the browser. 



-----------------------------------------------------------------------------------------------------------


API Reference:


- Backend URL: http:127.0.0.1:5000 (Localhost:5000)
- Frontend URL: http://127.0.0.1:3000 (Localhost:3000)


-----------------------------------------------------------------------------------------------------------


Error Handling:

Errors are returned using JSON format:

Example:

{
        "success": "False",
        "error": 404,
        "message": “Page not found”,
      }


-----------------------------------------------------------------------------------------------------------


Error codes returned/used are:

400 - Bad Request
404 - resource not found
422- unprocessable
500- internal server error


Authors
My amazing wife for all the help
Bob Kwon 
Udacity for including all of the front end and starter code
Pokemon API: from which i ripped off the formatting 


## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```