---
layout: ../../layouts/BlogLayout.astro
title: 'How to Install and Manage PostgreSQL on macOS'
published: 'March 4 2024'
tags: [database]
---

## Method 1: Installing PostgreSQL with Homebrew

Straightforward PostgreSQL setup for users who prefer the command-line.

### 1. Install PostgreSQL

Open Terminal and execute the following commands to update Homebrew and install PostgreSQL:

```sh
brew update
brew install postgresql
```

### 2. Start PostgreSQL Service

```sh
brew services start postgresql
```

PostgreSQL will run in the background as a service.

### 3. Creating a Database

To create a new database, you first need to connect to the PostgreSQL command-line interface (CLI):

```sh
psql -U postgres
```

Next, execute the command to create your database:

```sh
CREATE DATABASE my_new_database;
```

You can list all databases with command `\l`, or exit the CLI with `\q`.

### 4. Stopping PostgreSQL Service

When you're done and wish to stop the PostgreSQL service, use the following command:

```sh
brew services stop postgresql
```

## Method 2: Installing PostgreSQL Using the GUI Installer

If you're more comfortable with graphical interfaces, the PostgreSQL app and pgAdmin provide a user-friendly alternative to command-line tools.

### 1. Download PostgreSQL

Start by downloading the [PostgreSQL app](https://postgresapp.com/).

### 2. Download pgAdmin

To manage your databases via a GUI, download [pgAdmin](https://www.pgadmin.org/).

After installing both applications, you can create databases using pgAdmin and start your server with the PostgreSQL app.
