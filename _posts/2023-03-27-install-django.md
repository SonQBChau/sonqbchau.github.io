# Getting Started with Django Templates

Django is a popular Python web framework that provides a lot of useful features for building web applications. In this tutorial, we'll walk through the steps of setting up a new Django project with templates.

## Step 1: Create a Project Directory

The first step is to create a new project directory and navigate to it in your terminal. You can do this with the following commands:

```bash
Copy code
mkdir project_name
cd project_name
```

Replace project_name with the name of your project.

## Step 2: Set Up a Virtual Environment

Next, you'll want to create a virtual environment for your project. A virtual environment is a self-contained environment that allows you to install and manage dependencies for your project without affecting your system's global Python environment.

To create a virtual environment, use the following commands:

```bash
Copy code
python3 -m venv venv
source venv/bin/activate
```

## Step 3: Install Django

With your virtual environment activated, you can now install Django using pip. Run the following command to upgrade pip and install Django:

```bash
pip install --upgrade pip
pip install django
```

## Step 4: Create a New App

Now that Django is installed, you can create a new app. In Django, an app is a self-contained module that represents a specific feature or functionality of your project. To create a new app, use the following commands:

```bash
django-admin startproject config .
django-admin startapp app_name
```

Replace app_name with the name of your app.

## Step 5: Configure the App

Next, you need to add your app to the list of installed apps in config/settings.py. Open config/settings.py in your text editor and add the following line to the INSTALLED_APPS list:

```python
INSTALLED_APPS = [...'app_name',]
```

## Step 6: Create the Database

With your app configured, you can now create the database by running the following command:

```bash
python manage.py migrate
```

This will create the necessary database tables for your app.

## Step 7: Create a Superuser

Next, you'll want to create a superuser, which is an administrative user that has access to the Django admin interface. To create a superuser, run the following command:

```bash
python manage.py createsuperuser --email admin@example.com --username admin
```

Replace admin@example.com and admin with your own email address and username.

## Step 8: Run the Server

Finally, you can run the development server to test your app. Run the following command:

```bash
python manage.py runserver
```

This will start the development server at `http://localhost:8000/`. You can access the server in your web browser to see the default Django welcome page.

That's it! You've now set up a new Django project with templates.
