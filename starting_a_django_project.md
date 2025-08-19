Starting a Django Project

Learn how to create a full-stack Django app using Django Template Language (DTL) and PostgreSQL as your database.

## Table of Contents
1. Setting up PostgreSQL (and pgAdmin4)
2. Models, Views, and Templates
3. Understanding the Structure of a Django App

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


### Create a Database for the Project

Unlike MongoDB, which automatically creates a database the first time you use it, SQL databases require you to create the database manually before using it in a Django project.

#### Using the psql Command Line
Open the PostgreSQL shell:
```bash
psql
```

Create a new database for your project:
```bash
CREATE DATABASE catcollector_db;
```

### Using pgAdmin

- Open pgAdmin and connect to your PostgreSQL server.
- Right-click on Databases → Create → Database.
- Enter the database name (e.g., catcollector_db) and select an owner (user).
- Click Save.
