---
layout: ../../layouts/BlogLayout.astro
title: How to setup a python project with VS Code Dev Containers
published: 'Aug 5 2024'
tags: [vscode]
---

## How to setup a python project with VS Code Dev Containers

Setting up a Python project with a `.venv` is usually straightforward, especially when running the debugger directly from VS Code. However, integrating local services like PostgreSQL and Redis can be more complex. Fortunately, VS Code's Dev Containers make it easy to configure your development environment with these services.

## Setting Up Dev Containers

You can either use the built-in **Dev Containers: Add Dev Container Configuration Files** option or set up the configuration manually. Here's how to do it manually:

### Step 1: Create a `.devcontainer` Directory

In your project, create a `.devcontainer` directory and add the following `devcontainer.json` file:

```json
// For format details, see https://aka.ms/devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/postgres
{
 "name": "Python 3 & PostgreSQL",
 "dockerComposeFile": "docker-compose.yml",
 "service": "app",
 "workspaceFolder": "/workspaces/${localWorkspaceFolderBasename}"

 // Features to add to the dev container. More info: https://containers.dev/features.
 // "features": {},

 // Use 'forwardPorts' to make a list of ports inside the container available locally.
 // This can be used to network with other containers or the host.
 // "forwardPorts": [5000, 5432],

 // Use 'postCreateCommand' to run commands after the container is created.
 // "postCreateCommand": "pip install --user -r requirements.txt",

 // Configure tool-specific properties.
 // "customizations": {},

 // Uncomment to connect as root instead. More info: https://aka.ms/dev-containers-non-root.
 // "remoteUser": "root"
}
```

### Step 2: Set Up Docker Compose

Create a `docker-compose.yml` file to define your services:

```yaml
services:
  app:
    build:
      context: ..
      dockerfile: .devcontainer/Dockerfile

    volumes:
      - ../..:/workspaces:cached

    # Overrides default command so things don't shut down after the process ends.
    command: sleep infinity

    # Runs app on the same network as the database container, allows "forwardPorts" in devcontainer.json to function.
    network_mode: service:db

  db:
    image: postgres:latest
    restart: unless-stopped
    volumes:
      - postgres-data:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: postgres
      POSTGRES_DB: postgres
      POSTGRES_PASSWORD: postgres

  redis:
    image: redis:latest
    restart: unless-stopped
    ports:
      - "6379:6379"

volumes:
  postgres-data:
```

### Step 3: Create a Dockerfile

Add a `Dockerfile` to your `.devcontainer` directory to specify the development environment:

```dockerfile
FROM mcr.microsoft.com/devcontainers/python:1-3.11-bullseye

ENV PYTHONUNBUFFERED 1

# [Optional] If your requirements rarely change, uncomment this section to add them to the image.
# COPY requirements.txt /tmp/pip-tmp/
# RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
#    && rm -rf /tmp/pip-tmp

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
```

### Step 4: Open the Project in a Dev Container

Once you've set up the configuration files, you can use the **Dev Containers: Reopen in Container** option in VS Code. This will start your development environment inside a container, with PostgreSQL and Redis services running alongside your application.

Now, you can easily run the VS Code debugger with access to the database and other services, all contained within your development environment.
