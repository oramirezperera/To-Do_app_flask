# To-Do_app_flask
A To Do made in Flask, with Python, Mysql, HTML and CSS, this app uses [werkzeug](https://werkzeug.palletsprojects.com/en/1.0.x/) too.


## __init__.py
In app.config we use the .from_mapping because that allows us to define configuration variables that we can use in our app.
SECRET_KEY defines the sessions in our application.
A session is when we generate a key that we are going to send to the user, with this we can use it as a reference with data that is stored in the server. This is a cookie. 
Flask uses this string to create the sessions, in production this string needs to be more complicated.
Database host, is where you put the database. This will be passed as environment variables, using os.environ.get('FLASK_DATABASE_HOST'). This method will be used with the password and the username too.

after the configuration we import all the db

## Flask export

export FLASK_APP=todo, this exports the flask app and the value needs to be the containing folder.
export FLASK_ENV=development, this makes the development environment to the flask app, making it easier to see the changes in real time.

## db.py

imported mysql.connector
imported click, with this you can type commands direct in the terminal, we don't need to use mysql workbench to create, and make relations of the tables, we will do it directly from the terminal.
From flask import current_app keeps the app we are executing, import g is a that we will use in all the application you can assign different variables to g and then access to the variables in other parts of the app.
The user will be stored at g.
From flask.cli import with_appcontext this import is important because you will need it when we run the database, because when running the database you will need the context of the configuration of our app. With this you can access the database, user and password.
from .schema stores all the scripts that we will need to create the database.
close_db() closes the database so is not always open.
db = g.pop('db', None) extracts db from g so you can checkout if the db is None or not if db is not None it has to close 
init_app(app) you have to pass the argument app because you have to call the app that we created in __init__.py then after every request we will pass the close_db function.
init_db has all the logic we need to run the scripts that we define.
We decorate init_db_command() so we can assign a name to use it in the terminal.

## schema.py

if you want to delete tables and we want to do it inside this script we can't do this if the tables have foreign keys. If anyways you want to delete the tables you have to disable that validation and then reactivate it.
The password is varchar of 100 because we are going to encrypt the passwords.

## Flask modules

In flask the modules are like blueprints, for example auth module will be log in, auth and firewalls.
[functools](https://docs.python.org/3/library/functools.html) "The functools module is for higher-order functions: functions that act on or return other functions. In general, any callable object can be treated as a function for the purposes of this module."


## todo.py

We are protecting the routes and endpoints via the login_required() function. This is a decorator function.
With load_logged_in_user puts the user in g, this function checks if the user is registered and if not, sends you to the register page.
