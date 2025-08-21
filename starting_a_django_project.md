# Starting a Django Project

Learn how to create a full-stack Django app using Django Template Language (DTL) and PostgreSQL as your database.

## Table of Contents
1. Setting up PostgreSQL (and pgAdmin4)
2. Models, Views, and Templates
3. Starting Your Project
4. Connecting to DB
5. URLs (Routing)
6. Views
7. Templates


## Setting up PostgreSQL
It is a powerful, open-source relational database system. We'll use it as the backend database for our Django project.

### Install PostgreSQL
- macOS (with Homebrew):
```bash
brew install postgresql
brew services start postgresql
```
Windows: Download the installer from [postgresql.org](https://www.postgresql.org/download/windows/) and follow the instructions.

---
 
### Install pgAdmin (Optional GUI)

*pgAdmin* is a graphical interface for managing PostgreSQL databases, similar to MongoDB Compass, which is the GUI for MongoDB.

Key difference: PostgreSQL is relational (tables, rows, foreign keys), while MongoDB is NoSQL (documents, collections, JSON-like structure).

---
 
### Install psycopg2
To use PostgreSQL, we need to do a one-time install of the psycopg2 Python package:
```bash
pipenv install psycopg2-binary
```
psycopg2 is a popular library that enables Python applications to interface with PostgreSQL.

---
 
### Create a Database for the Project

Unlike MongoDB, which automatically creates a database the first time you use it, SQL databases require you to create the database manually before using it in a Django project. You can either use psql shell, createdb, or pgAdmin.

#### Using the psql Command Line
Open the PostgreSQL shell:
```bash
psql
```

Create a new database for your project:
```bash
CREATE DATABASE catcollector_db;
```

Exit using
```bash
\q
```

### Using createdb
```bash
createdb catcollector_db
```

This creates a new database named catcollector_db. You don’t need to open the psql shell first — it runs directly from your terminal.

### Using pgAdmin

- Open pgAdmin and connect to your PostgreSQL server.
- Right-click on Databases → Create → Database.
- Enter the database name (e.g., catcollector_db) and select an owner (user).
- Click Save.


## Models, Routes and Controllers

- Models: define the structure and behavior of the data in your Django application. **Just like the Models in MVC!**

- Views: handle the logic for a specific request. They process incoming requests, retrieve or modify data via models, and decide what data to send to the user. **Just like the Controllers in MVC!**

- Templates: define how the data is presented to the user. They are HTML files with placeholders for dynamic content. Templates handle the “view” part in the front end, formatting data provided by views. **Just like Views in MVC!**



<img width="1233" height="638" alt="image" src="https://github.com/user-attachments/assets/7898c0d2-fe6b-4301-8070-b0aff8d55595" />

## Starting Your Project

### Start a new Django project
```bash
django-admin startproject project_name 
cd project_name
```

Run the development server
```bash
python manage.py runserver
```

<details><summary>Project 🏠 vs. App 🛋️</summary>

Project = the overall Django website (settings, URLs, config). It's the whole house 🏠 (with wiring, foundation, and rooms).

App = a modular feature inside the project. each room 🛋️ (kitchen, bedroom, bathroom). Each has a purpose but they all belong to the house.

A project can contain many apps, but every app lives inside a project.

</details>

Visit `http://127.0.0.1:8000/` in your browser to see your Django site.

When you're done working on your project, you can deactivate the pipenv shell by typing:

```bash
exit
```

This should be your structure so far:
<br>
<img width="152" height="339" alt="image" src="https://github.com/user-attachments/assets/68d58c62-047f-43f0-982b-308468f2bc72" />
<br>

Let's take a look at `catcollector` project folder first.

```tree
catcollector/
├── manage.py
├── catcollector/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
```

- `manage.py` → run commands
- `__init__.py` → makes the folder a Python module
- `settings.py` → project configuration
- `urls.py` → URL routing
- `wsgi.py` → production entry point (WSGI)
- `asgi.py` → production entry point (ASGI, async support)

Most important ones right now will be manage.py, settings.py and urls.py

---

### Start a new app
```bash
python manage.py startapp main_app
```

You’ll see a new folder called `main_app` with this structure:
```tree
main_app/
├── __init__.py
├── admin.py
├── apps.py
├── migrations/
│   └── __init__.py
├── models.py
├── tests.py
└── views.py
```

- `models.py` → database tables
- `views.py` → logic for requests/responses
- `admin.py` → connect models to Django Admin
- `apps.py` → app config
- `migrations/` → DB history changes
- `tests.py` → automated tests


Most important ones right now will be models.py, views.py and urls.py

Include your app in your catcollector project by adding it to **INSTALLED_APPS** in `settings.py`:
<img width="287" height="203" alt="image" src="https://github.com/user-attachments/assets/1afb907e-f93f-4348-bd70-609673a519c7" />


## Connecting to Database
Earlier we created a dedicated catcollector PostgreSQL database.

A Django project's configuration lives in `settings.py`. To set up our database, scroll down to:

<br>
<img width="379" height="111" alt="image" src="https://github.com/user-attachments/assets/4aa36748-f4e4-49ff-8739-ceae06db7420" />
<br>

Change it to:
🚨 Don't follow blindly! Actually input the proper details. 🚨

<br>
<img width="605" height="182" alt="image" src="https://github.com/user-attachments/assets/5623d7a9-9b6f-42e9-83aa-cb745dfc9a5e" />
<br>

> Django defaults to SQLite, which isn’t suited for production. Update your project settings to use PostgreSQL instead.


If you run the server, you'll see an error about unapplied migration message:

<br>
<img width="958" height="113" alt="image" src="https://github.com/user-attachments/assets/37d5dd7d-a1c8-41d9-8ea2-73455827a022" />
<br>

To get rid of it, let's apply our migrations with

```bash
python3 manage.py migrate
```

## URL Routing in Django

In Express, every incoming request needs a matching route, and that route determines which function runs in response. Django works similarly, but with a slightly different approach:

- Routes in Django match only the URL path — the HTTP method (GET, POST, etc.) is not part of the matching process. You’ll handle the request method inside the view function instead.
- All routes are defined in URL configuration files (called urls.py), which act as a roadmap for directing requests to the right views.

### Setting Up the Home Page

Let’s wire up the root URL so that visiting:
```bash
http://localhost:8000
```

loads the home page of the app.
<br>
<img width="1186" height="713" alt="image" src="https://github.com/user-attachments/assets/8a4e4039-c162-4919-8ff5-09af4bd74db5" />
<br>

#### 1. Prepare the URL configuration

Every Django project includes a central URL configuration — in our case, that’s:
```bash
catcollector/
  urls.py
```

While you could dump all your routes there, the recommended practice is to keep each app’s routes organized in its own urls.py file, then “plug in” that file to the main project-level configuration.

---
##### Create a urls.py for the app
Run this command inside the main_app directory:
```bash
touch main_app/urls.py
```
This creates a blank URL configuration file specifically for the main_app.

---
##### Include the app routes in the project-level file
Open the project’s catcollector/urls.py and update it like this:
```py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('main_app.urls')),  # Send root requests to main_app
]
```
Now, any request to / will look for matching patterns in main_app/urls.py.

#### 2. Define the route
Inside main_app/urls.py, add this:
```py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

- `urlpatterns` → List of URL routes for the app.
- `path('')` → Matches the root URL (/).
- `views.home` → Calls the home view function when / is requested.
- `name='home'` → Gives the route a name for easy reference in templates or with reverse(). 

<details><summary>Why `name='home'?`</summary>
In a Django template, instead of hardcoding a URL like this:
 
```html
<a href="/">Home</a>
```

You can use:
```html
<a href="{% url 'home' %}">Home</a>
```

If the route ever changes (say, from / to /dashboard), you only need to update it in urls.py, and every reference will still work — that’s the main benefit of naming routes.

</details>

#### 3. Write the view function
Finally, in main_app/views.py, create a simple view to handle requests to /:

```py
from django.http import HttpResponse

def home(request):
    return HttpResponse("<h1>Welcome to Cat Collector!</h1>")
```

### Django vs. Express: A Quick Snapshot
| Feature | **Django** | **Express** |
|----------|------------|-------------|
| **Route storage** | Defined in `urls.py` for each app, plus a main project-level `urls.py`. | Typically in `app.js` or separate files inside a `routes/` folder. |
| **URL matching** | Matches **only the path**; the HTTP method is handled in the view logic. | Matches **path and HTTP method** directly (e.g., `app.get`, `app.post`). |
| **Handling methods** | Use conditional checks in the view (e.g., `if request.method == "POST":`). | Handled by method-specific functions like `app.get()` or `app.post()`. |
| **Dynamic URLs** | Uses converters like `<int:id>` or regex with `re_path()`. | Uses route parameters like `/:id` with optional regex patterns. |
| **Link generation** | Built-in helpers like `reverse()` in Python or `{% url 'name' %}` in templates. | Typically manual string building or third-party helper libraries. |
