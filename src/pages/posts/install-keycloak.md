---
layout: ../../layouts/BlogLayout.astro
title: 'How to Set Up Keycloak'
published: 'March 28 2024'
tags: [keycloak]
---

This guide will take you through the process of settting up Keycloak using Docker and scripts that handle external credentials. You should have Docker installed on your system before beginning.

### Step 1: Prepare Your Docker Compose

Creating a Docker Compose file is the first step. This file outlines how your Keycloak service will operate. To avoid hardcoding credentials into the Docker Compose file, we utilize a [credential_loader](https://github.com/SonQBChau/keycloak-setup/blob/main/src/scripts/credential_loader.sh). This script dynamically loads the admin username and password from a secret file when the container starts. This method improves security and simplifies credential management.

### Step 2: Run Keycloak Setup Script

After your container is up, the next step is running the [keycloak_setup](https://github.com/SonQBChau/keycloak-setup/blob/main/src/scripts/keycloak_setup.sh) script. This script makes use of `kcadm.sh`, a command-line tool within Keycloak, to authenticate as an admin. It allows you to perform initial setup tasks that could alternatively be done using the [Keycloak portal](https://www.keycloak.org/getting-started/getting-started-docker). Additionally, this script handles the setup of realms, clients, and users.

### Step 3: Create Realm

The [realm_setup](https://github.com/SonQBChau/keycloak-setup/blob/main/src/scripts/realm_setup.sh) script establishes a "realm" for your application. A realm in Keycloak acts as a container for managing users, credentials, roles, and groups. It manages your application's in an isolated environment.

### Step 4: Create Your Application Client

Setting up application client achieved through the [client_setup](https://github.com/SonQBChau/keycloak-setup/blob/main/src/scripts/client_setup.sh) script. This script defines client scope, and managing access and permissions. It handles how your application interacts with Keycloak, including redirect URIs, client roles, and more, ensuring secure and controlled access.

### Step 5: User Setup

The final step involves creating users through the [user_setup](https://github.com/SonQBChau/keycloak-setup/blob/main/src/scripts/client_setup.sh) script, which will update the passwords securely from a secret.

### Logging Into Your Keycloak

With the steps completed, you can test the application on the [Keycloak website](https://www.keycloak.org/app/). The client_setup script includes configuring this redirect URL.

You can find all the source codes [here](https://github.com/SonQBChau/keycloak-setup)
