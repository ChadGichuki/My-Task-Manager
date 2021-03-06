# My-Task-Manager

# Video Demo
This project is my CS50x 2022 final project submission. 
Here is a link to a demo of the project: https://youtu.be/TEz5YAL_1eA


# Overview
This is a web app where you can keep track of the tasks you need to accomplish everyday.

The app allows you to register with a unique username and passwords afterwhich you can login and logout at any time. Once logged in, the session will keep you logged in for a day. You can add a task and specify a deadline by which to carry out the task. All the tasks yet to be completed will be displayed on the Tasks page including the date added and the deadline. For each task you have the option to delete, update or mark as completed. All completed tasks appear on the archives page.

Just to get you going, there is a motivation page where you can read a different motivational quote everyday.


# Installation
There isn't musch to this, just:
1. Clone this repository.
   
    ``` $ git clone https://github.com/ChadGichuki/My-Task-Manager ```

2. Navigate to the project directory.

    ``` $ cd Task-Master```


# Technologies and Libraries
1. Flask - The backend is implemented using Flask library. This also includes Flask-migrate for migrating the database and Flask-SQLAlchemy for use of SQLAlchemy to query the db.
2. SQLAlchemy - This toolkit was used for Object Relational Mapping and implementing SQL queries in python language. I initially thought of using SQL commands but after research decided to use SQLAlchemy which is capable of complex queries and mappings in a scalable way. 
3. Werkzeug - This library was used for hashing of passwords as well as verification of passwords before logging in.
4. Requests - This library was used to communicate with the quotepub API for daily motivational quotes.
5. Sqlite - Seeing that this is a small-scale project, I opted to use sqlite for the Relational database management system.
6. Bootstrap - Took advantage of this CSS framework to implement a responsive mobile-first site as well as fun and user-friendly features like the Navbar, tables and cards.


# Features
The following main features are implemented as routes (@app.route) in app.py:
- **Home Page**: On this page, the user can see all the tasks they are yet to complete including the date the task was added and the due date for the task. A user can also add a new task for the day. The user can see their username displayed for a personal feel. Handles both GET and POST requests.
- **Delete Task**: If the task is no longer necessary, a user may delete that task from their list. Only handles GET requests.
- **Update Task**: A task can be updated to change the details of the task or the due date. Handles both GET and POST requests.
- **Complete Task**: Once completed, the joy is in marking a task as completed and having it disappear from the list of tasks. Only handles GET requests.
- **Archives**: This is a page where all the completed tasks are displayed. I believe this is necessary for the user's sense of satisfaction. Only handles GET requests.
- **Motivation**: This page displays a motivational quote sourced from quotepub API. We all need motivational to remain productive and complete our tasks. Only handles GET requests.
- **Login**: A user can login to their account from any device using their unique username and password. Handles both GET and POST requests.
- **Logout**: A user can logout at any time. The session keeps them logged in for 1 day after which they are automatically logged out. Only handles GET requests.
- **Register**: A new user can sign up and have full access to the Task Master features. Handles both GET and POST requests.

There are 2 helping funtions in functions.py:
- **Login_required**: Restricts access to features of the app if a user is not logged in.
- **get_quote**: Contacts the quotepub API and parses the JSON repsonse for the daily motivational quote.

The following html templates have been used to build the web pages:
- **Base.html**: All other templates inherit from this base file. It contains the necessary meta, script & link tags to load bootstrap and the static files. It also contains the Navbar as well as {% block head %} and {% block body %} blocks.
- **Index.html**: Has a table to display all tags and a form to add tasks and deadlines. Also has a div to diplay the logged in user's username.
- **Archives.html**: Has a table to display all the archived tasks
- **Motivation.html**: Has a div of class="card" which displays an inspiring image and a motivational quote from quotepub API. Includes a link to the tasks page.
- **Update.html**:
- **Login.html**: Has a form to enter a username and password.
- **Register.html**: Has a form to enter a username, password and password confirmation.

# The Database
The tasks.db schema has 3 tables:


- CREATE TABLE todo (
	id INTEGER NOT NULL, 
	user_id INTEGER, 
	content VARCHAR(200) NOT NULL, 
	deadline DATETIME, 
	date_added DATETIME, 
	PRIMARY KEY (id), 
	FOREIGN KEY(user_id) REFERENCES users (id)
)

- CREATE TABLE users (
	id INTEGER NOT NULL, 
	username VARCHAR(200) NOT NULL, 
	hash VARCHAR NOT NULL, 
	PRIMARY KEY (id)
)

- CREATE TABLE archives (
	id INTEGER NOT NULL, 
	user_id INTEGER, 
	content VARCHAR(200) NOT NULL, 
	date_completed DATETIME, 
	PRIMARY KEY (id), 
	FOREIGN KEY(user_id) REFERENCES users (id)
)

# Deployment
I deployed the project to heroku. To do this you need to:
1. Sign up on Heroku. https://signup.heroku.com/login
2. Use the Free tier because we're only using sqlite.
3. Install the heroku CLI. https://devcenter.heroku.com/articles/heroku-cli
4. Install gunicorn ```$ pip install gunicorn```
5. Create a Procfile
6. Create a requirements.txt file ```$ pip freeze > requirements.txt```
7. Create a local git repository, add all and commit.
8. Create your heroku app. ```$ heroku create unique-name-of-app```
9. If successful, push to heroku ```$ git push heroku main```