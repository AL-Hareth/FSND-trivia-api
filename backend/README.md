# Full Stack Trivia API Backend

## Getting Started
 
### Installing Dependencies

#### Python 3.7

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
This README is missing documentation of your endpoints. Below is an example for your endpoint to get all categories. Please use it as a reference for creating your documentation and resubmit your code. 

Endpoints
GET '/categories'
GET ...
POST ...
DELETE ...

GET '/categories'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a single key, categories, that contains a object of id: category_string key:value pairs. 
{'1' : "Science",
'2' : "Art",
'3' : "Geography",
'4' : "History",
'5' : "Entertainment",
'6' : "Sports"}

```

## Documentation

# Installing the project

```
git clone https://github.com/AL-Hareth/FSND-trivia-api.git
```

setup the Database:
```
psql trivia < trivia.psql
```

Then go to the cloned folder and start a virtual environment using:
```
pip install virtualenv
virtualenv mypython
```
Now to activate the virtual environment:
MacOS/Linux:
```
source mypython/bin/activate
```
Windows:
```
cd env/Scripts
activate
```

In order to deactivate the environment:
```
deactivate
```

Now to run the flask app you have to install the dependenciese:
```
pip3 install -r requirments.txt
```
Set your app variables:
MacOS/Linux:
```
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```
Windows:
```
set FLASK_APP=flaskr
set FLASK_ENV=development
flask run
```
And now you're good to go.

# Requests and Responses
Get paginated questions (10 every page)
```
curl 127.0.0.1:5000:questions
```
Returns:
```
{
          'success': True,
          'questions': <list of 10 questions>,
          'total_questions': <the total of all questions in the database>,
          'current_category': <the current category which the questions are fetched from>,
          'categories': <all categories' names>
}
```

Get questions in specific page
```
curl 127.0.0.1:5000/questions?page=<page_number>
```
Returns:
```
{
          'success': True,
          'questions': <list of 10 questions in the second page>,
          'total_questions': <the total of all questions in the database>,
          'current_category': <the current category which the questions are fetched from>,
          'categories': <all categories' names>
}
```

Get questions by category
```
curl 127.0.0.1:5000/questions?current_category=<category_id>
```
Returns:
```
{
          'success': True,
          'questions': <list of 10 questions>,
          'total_questions': <the total of all questions in this specific category of the database>,
          'current_category': <the current category which the questions are fetched from>,
          'categories': <all categories' names>
}
```

Delete question by ID
```
curl -X DELETE 127.0.0.1:5000/questions/<question_id>
```
Returns:
```
{
        'success': True,
        'message': 'deleted question <question_id>'
}
```

Create new question
```
curl -X POST -d {<json_data>} 127.0.0.1:5000/questions
```
<json_data> should contain: "question", "answer", "difficulty", "category"
Returns:
```
{
        'success': True,
        'question': <inserted_question>,
        'answer': <inserted_answer>,
        'difficulty': <inserted_difficulty>,
        'category': <inserted_category>
}
```

Search a question by substring
```
curl -X POST -d {<json_data>} 127.0.0.1:5000/questions/search
```
<json_data> should contain the "searchTerm"
Returns:
```
{
        "success": True,
        "questions": <list of questions that match the search term>
}
```

Play the quiz game
```
curl -X POST -d {<category>, <previous_questions>} 127.0.0.1:5000/play
```
<category> contains: {"id": <category_id>, "type": <category_type>}
<previous_questions> contains an Array of previous questions IDs
Returns:
 ```
{
        "success": True,
        "question": {
          "id": <question_id>,
          "question": <question_question>,
          "answer": <question_answer>,
          "category": <question_category>,
          "difficulty": <question_difficulty>
        }
}
 ```

# The Errors Documentation:

- 404 [Page not found]: This error code means that you're requesting an endpoint that doesn't exist.
- 400 [Bad request]: The request contains invalid syntax.
- 405 [Method not allowed]: It means you're using a method that is not supported for this particular endpoint.
- 422 [Unproccessable entity]: Your request body has the correct syntax but it contains semantic errors.
- 500 [Internal server error]: This error means that the Server can't handle the code.



## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
