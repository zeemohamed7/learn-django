# Starting a Django Project

Learn how to create a full-stack Django app using Django Template Language (DTL) and PostgreSQL as your database.

## Table of Contents
1. Setting up PostgreSQL (and pgAdmin4)
2. Models, Views, and Templates
3. Starting Your Project
4. 
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

---

### Install pgAdmin (Optional GUI)

*pgAdmin* is a graphical interface for managing PostgreSQL databases, similar to MongoDB Compass, which is the GUI for MongoDB.

Key difference: PostgreSQL is relational (tables, rows, foreign keys), while MongoDB is NoSQL (documents, collections, JSON-like structure).

### Install psycopg2
To use PostgreSQL, we need to do a one-time install of the psycopg2 Python package:
```bash
pipenv install psycopg2-binary
```
psycopg2 is a popular library that enables Python applications to interface with PostgreSQL.

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

---
## Models, Routes and Controllers

- Models: define the structure and behavior of the data in your Django application. **Just like the Models in MVC!**

- Views: handle the logic for a specific request. They process incoming requests, retrieve or modify data via models, and decide what data to send to the user. **Just like the Controllers in MVC!**

- Templates: define how the data is presented to the user. They are HTML files with placeholders for dynamic content. Templates handle the “view” part in the front end, formatting data provided by views. **Just like Views in MVC!**

<img width="1233" height="638" alt="image" src="https://github.com/user-attachments/assets/7898c0d2-fe6b-4301-8070-b0aff8d55595" />
---
## Starting Your Project
