# Setup and Installation

In this tutorial, I will walk you through the process of setting up Django, a powerful Python web framework, using Pipenv for managing packages and virtual environments and PostgreSQL


> ⚠️ Note: This is mostly based on macOS, so commands might vary. I am also using pipenv to automatically create virtual environments instead of installing packages system-wide to avoid breaking anything.

## Table of Contents
- [Key Tools](#key-tools)
- [Setting up](#setting-up)
- [Installing Django with Pipenv](#installing-django-with-pipenv)
- [Setting up PostgreSQL (and pgAdmin4)](#setting-up-postgresql)
- [Notes & Tips](#notes--tips)  

## Key Tools
### Pip
- Python’s package manager, similar to npm for JavaScript. 
- Used to install and manage Python libraries.

### venv
- Used to create isolated Python environments so that project dependencies don’t conflict.
- Packages installed in a virtual environment stay separate from your system Python.

### Pipenv
- Combines the power of pip and venv!
- Automatically creates and manages a virtual environment for each project.
- Handles package installations and keeps track of dependencies using:
- Pipfile – specifies project dependencies
- Pipfile.lock – locks exact versions for reproducibility

> Remember seeing something similar in wih Node.js?
---
## Setting up

### Install Python 3
#### ⚠️ Note: this only needs to be done once, if you’ve done this before, skip this step!

1. Check if you already have Python installed:
```bash
python3 --version
```

If you see a verison above 3.11, you're good! 

If not:
- macOS (with Homebrew):
```bash
brew install python
```
- Windows: Download and install from [python.org/downloads](https://www.python.org/downloads/)

> When you install a new version of Python, sometimes your system still points python3 to the old one. This is because your PATH is still mapped to the older Python binary. Consult your instructor on this! 

### Install Pipenv
Install it once on your system:

#### macOS
```bash
brew install pipenv
```

#### or everywhere (with pip)
```bash
pip install pipenv --user
```

If pipenv isn’t recognized after installing with pip, add it to your PATH:
```bash
export PATH="$(python3 -m site --user-base)/bin:$PATH"
```

Verify installations:
```bash
python3 --version   # should show Python 3.x
pipenv --version    # should show Pipenv x.x.x
```

### Installing Django with Pipenv
Create a project folder
```bash
mkdir my_django_project
cd my_django_project
```

Install Django and create a virtual environment
```bash
pipenv install django
```
Pipfile and Pipfile.lock should be created.


Activate the virtual environment
```bash
pipenv shell
```
Being in the shell looks like this:

<br>
<img width="359" height="33" alt="image" src="https://github.com/user-attachments/assets/06cfeca9-0631-447f-a276-e94b5fdb52a8" />
<br>
<br>

Verify the installation:
```bash
django-admin --version
```

Now you’re ready to run Django commands inside your project!

---
## Setting up PostgreSQL
It is a powerful, open-source relational database system. We'll use it as the backend database for our Django project.

### Install PostgreSQL
- macOS (with Homebrew):
```bash
brew install postgresql
brew services start postgresql
```
Windows: Download the installer from [postgresql.org](https://www.postgresql.org/download/windows/) and follow the instructions.

To use PostgreSQL, we need to do a **one-time install** of the psycopg2 Python package:
```bash
pip3 install psycopg2-binary
```
psycopg2 is a library that allows Python applications to interface with PostgreSQL.

### Install pgAdmin (Optional GUI)

pgAdmin is a graphical interface for managing PostgreSQL databases.

You can create databases, users, and run SQL queries without using the command line.

It’s similar to MongoDB Compass, which is the GUI for MongoDB.

Key difference: PostgreSQL is relational (tables, rows, foreign keys), while MongoDB is NoSQL (documents, collections, JSON-like structure).

### Install psycopg2
To use PostgreSQL, we need install of the **psycopg2** Python package:
```bash
pipenv install psycopg2-binary
```
**psycopg2-binary** is a popular library that enables Python applications to interface with PostgreSQL.

### Create a Database for the Project

Unlike MongoDB, which automatically creates a database the first time you use it, SQL databases require you to create the database manually before using it in a Django project. You can either use **psql shell, createdb, or pgAdmin.**

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

---
### Notes & Tips

- Always use Pipenv for managing packages and environments.

- Keep track of your dependencies in the Pipfile.

- You don’t need to activate the virtual environment to install packages with Pipenv (pipenv install package_name).

- Activate the shell (pipenv shell) when running Django commands interactively.

> ⚠️ Note that if you run the `django-admin --version` command again, you'll receive a message that it's not installed. Packages only work within the environment they were installed in!
