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


## API

GET `\categories` 
Fetches a dictionary of all available categories
- *Request parameters:* none 
- *Example response:* 
```
{
  "categories": {
    "1": "Math", 
    "2": "Art", 
    "3": "Sports", 
    "4": "History", 
    "5": "Entertainment"
  }, 
  "success": true
}

```


GET `\questions?page=<page_number>` 
Fetches a paginated dictionary of questions of all available categories
- *Request parameters (optional):* page:int 
- *Example response:*  
 ``` {
  "categories": {
    "1": "Math", 
    "2": "Art", 
    "3": "Sports", 
    "4": "History", 
    "5": "Entertainment" 
  }, 
  "current_category": null, 
  "questions": [
    {
      "answer": "20", 
      "category": 1, 
      "difficulty": 2, 
      "id": 5, 
      "question": "4 * 5 ?"
    },  
    {
      "answer": "75", 
      "category": 1, 
      "difficulty": 2, 
      "id": 16, 
      "question": "50 * 1.5 ?"
    }
  ], 
  "success": true, 
  "total_questions": 2
}
```

DELETE `/questions/<question_id>`
Delete an existing questions from the repository of available questions
- *Request arguments:* question_id:int 
- *Example response:* 
```
{
  "deleted": "28", 
  "success": true
}
```

POST `/questions`
Add a new question to the repository of available questions
- *Request body:* {question:string, answer:string, difficulty:int, category:string}
- *Example response:* 
```
{
  "created": 29, 
  "success": true
}
```
POST `/questions/search`
Fetches all questions where a substring matches the search term (not case-sensitive)
- *Request body:* {searchTerm:string}
- *Example response:*
```
{
  "current_category": null, 
  "questions": [
    {
       "answer": "20", 
       "category": 1, 
       "difficulty": 1, 
       "id": 1, 
       "question": "5 * 4 ="
    }
  ], 
  "success": true, 
  "total_questions": 1
}
```

GET `/categories/<int:category_id>/questions`
Fetches a dictionary of questions for the specified category
- Request argument: category_id:int
- response:
```
{
  "current_category": 1, 
  "questions": [
    {
       "answer": "20", 
       "category": 1, 
       "difficulty": 1, 
       "id": 1, 
       "question": "5 * 4 ="
    }, 
    {
       "answer": "20", 
       "category": 1, 
       "difficulty": 1, 
       "id": 1, 
       "question": "5 * 4 ="
    }, 
  ], 
  "success": true, 
  "total_questions": 2
}
```
POST `/quizzes`
Fetches one random question within a specified category. Previously asked questions are not asked again. 
-Request body: {previous_questions: arr, quiz_category: {id:int, type:string}}
- response: 
```
{
  "question": {
    "answer": "20", 
    "category": 1, 
    "difficulty": 1, 
    "id": 1, 
    "question": "5 * 4 ="
  }, 
  "success": true
}
```

## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
