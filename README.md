# Django with Pipenv: A Beginner's Guide

This guide will help you set up Python and Django, a powerful Python web framework, using Pipenv for managing packages and virtual environments.
In this tutorial, I will walk you through the process of setting upDjango, a powerful Python web framework, using Pipenv for managing packages and virtual environments.


> ⚠️ Note: This is mostly based on macOS, so commands might vary.

## Table of Contents
- [Key Tools](#key-tools)
- [Setting up](#setting-up)
- [Installing Django with Pipenv](#installing-django-with-pipenv)
- [Django Project Basics](#django-project-basics)
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

### macOS
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

Verify Installations
Check that both work:
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
Being in the shell looks liek this:
<br>
<img width="359" height="33" alt="image" src="https://github.com/user-attachments/assets/06cfeca9-0631-447f-a276-e94b5fdb52a8" />
<br>

Now you’re ready to run Django commands inside your project!

Verify the installation:
```bash
django-admin --version
```

### Django Project Basics

Start a new project
```bash
django-admin startproject project_name
cd project_name
```

Start a new app
```bash
python manage.py startapp app_name
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

Visit http://127.0.0.1:8000/ in your browser to see your Django site.

When you're done working on your project, you can deactivate the pipenv shell by typing:
```bash
exit
```

4. Notes & Tips

Always use Pipenv for managing packages and environments.

Keep track of your dependencies in the Pipfile.

You don’t need to activate the virtual environment to install packages with Pipenv (pipenv install package_name).

Activate the shell (pipenv shell) when running Django commands interactively.

> ⚠️ Note that if you run the `django-admin --version` command again, you'll receive a message that it's not installed. Packages only work within the environment they were installed in!
