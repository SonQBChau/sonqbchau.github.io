---
layout: ../../layouts/BlogLayout.astro
title: 'How to install Django for development on MacOS'
published: 'March 27 2023'
modified: 'March 04 2024'
tags: [django]
---

## Step 1: Create a Project Directory

The first step is to create a new directory for your project and navigate into it. Replace `project_name` with the actual name of your project.

```bash
mkdir project_name
cd project_name
```

## Step 2: Set Up a Virtual Environment

Creating a virtual environment is crucial as it allows you to manage project-specific dependencies without affecting the global Python environment on your system.

To create a virtual environment, run:

```bash
python3 -m venv venv
source venv/bin/activate
```

## Step 3: Install Django

With the virtual environment active, install Django using `pip`:

```bash
pip install --upgrade pip
pip install django
```

## Step 4: Create a New Project and App

Django organizes its applications in projects. A project encompasses the configuration and apps for a specific website. An app is a web application that does something – e.g., a blog, a database of public records, or a simple poll app.

First, create a new Django project:

```bash
django-admin startproject config .
```

Then, create a new app within your project (replace `app_name` with your app's name):

```bash
django-admin startapp app_name
```

## Step 5: Configure the App

Add your new app to the `INSTALLED_APPS` list in `config/settings.py` to include it in your project:

```python
INSTALLED_APPS = [
    ...,
    'app_name',
]
```

## Step 6: Create a Superuser

Create a superuser for accessing the Django admin interface. Replace `admin@example.com` and `admin` with your preferred email and username:

```bash
python manage.py createsuperuser --email admin@example.com --username admin
```

## Step 7: Configure a Database (Optional)

**Prerequisite**: Ensure that PostgreSQL is installed on your local machine. If it's not, you can follow this [setup PostgreSQL guide](https://sonqbchau.github.io/posts/django-postgres/).

Django uses SQLite by default, but if you prefer PostgreSQL, modify `config/settings.py` as follows:

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "database_name",
        "USER": "admin_username",
        "PASSWORD": "admin_password",
        "HOST": "localhost",
        "PORT": "5432",
    }
}
```

Add psycopg driver:

```bash
pip install 'psycopg[binary]'
```

Apply migrations to create the necessary tables:

```bash
python manage.py makemigrations
python manage.py migrate
```

## Step 8: Run the Server

To start the development server and test your setup, execute:

```bash
python manage.py runserver
```

This command starts the server on `http://localhost:8000/`. If you can see the Django welcome page, you have successfully set up a new Django project!
