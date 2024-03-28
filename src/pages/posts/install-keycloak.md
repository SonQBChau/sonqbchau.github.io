---
layout: ../../layouts/BlogLayout.astro
title: 'How to Set Up Keycloak'
published: 'March 28 2024'
tags: [keycloak]
---

This guide will take you through the process of settting up Keycloak using Docker and scripts that handle external credentials. You should have Docker installed on your system before beginning.

### Step 1: Prepare Docker Compose

Creating a Docker Compose file is the first step. This file outlines how your Keycloak service will operate. To avoid hardcoding credentials into the Docker Compose file, we utilize a [credential_loader](https://github.com/SonQBChau/keycloak-setup/blob/main/src/scripts/credential_loader.sh). This script dynamically loads the admin username and password from a secret file when the container starts and simplifies credential management.

```sh
# Load credentials from secrets
export KEYCLOAK_ADMIN=$(< /run/secrets/kc-admin-user)
export KEYCLOAK_ADMIN_PASSWORD=$(< /run/secrets/kc-admin-password)
```

### Step 2: Run Keycloak Setup Script

After your container is up, the next step is running the [keycloak_setup](https://github.com/SonQBChau/keycloak-setup/blob/main/src/scripts/keycloak_setup.sh) script. `kcadm.sh` is a command-line tool within Keycloak to authenticate as an admin. It allows you to perform initial setup tasks that could alternatively be done using the [Keycloak portal](https://www.keycloak.org/getting-started/getting-started-docker). Additionally, this script calls the setup of realms, clients, and users.

```sh
# authenticate as admin
KCADM config credentials --server $KC_ADMIN_URL --user $KEYCLOAK_ADMIN --password $KEYCLOAK_ADMIN_PASSWORD --realm master

# create realm
source ./realm_setup.sh
# create client
source ./client_setup.sh
# create test users
source ./user_setup.sh
```

### Step 3: Create Realm

The [realm_setup](https://github.com/SonQBChau/keycloak-setup/blob/main/src/scripts/realm_setup.sh) script establishes a "realm" for your application. A realm in Keycloak acts as a container for managing users, credentials, roles, and groups. It manages your application's in an isolated environment.

```sh
KCADM create realms -s realm="$KEYCLOAK_REALM" -s enabled=true
```

### Step 4: Create Client

Setting up application client achieved through the [client_setup](https://github.com/SonQBChau/keycloak-setup/blob/main/src/scripts/client_setup.sh) script, which defines client scope, and managing access and permissions. It handles how your application interacts with Keycloak, including redirect URIs, client roles, and more, ensuring secure and controlled access.

```sh
KCADM create clients -r "$REALM_NAME" -s clientId="$CLIENT_ID" -s enabled=true
```

### Step 5: Create User

The final step is creating users through the [user_setup](https://github.com/SonQBChau/keycloak-setup/blob/main/src/scripts/client_setup.sh) script, which will update the passwords securely from secrets.

```sh
initUser() {
    local USER_NAME=$1
    local PASSWORD=$2
    local EMAIL=$3
    local FIRST_NAME=$4
    local LAST_NAME=$5

    local USER_ID=$(createUser "$KEYCLOAK_REALM" "$USER_NAME")
    if [[ -n "$USER_ID" ]]; then
        KCADM update users/$USER_ID -r "$KEYCLOAK_REALM" -s firstName="$FIRST_NAME" -s lastName="$LAST_NAME" -s email="$EMAIL"
        KCADM set-password -r "$KEYCLOAK_REALM" --username "$USER_NAME" --new-password "$PASSWORD"
    fi
}

# params: username password email firstname lastname
initUser "$(cat ../secrets/kc-user1.txt)" "$(cat ../secrets/kc-user1-password.txt)" "user1@test.ca" "One" "User"
initUser "$(cat ../secrets/kc-user2.txt)" "$(cat ../secrets/kc-user2-password.txt)" "user2@test.ca" "Two" "User"
```

### Step 6: Testing

With the steps completed, you can test the application on the [Keycloak website](https://www.keycloak.org/app/). The client_setup script includes configuring this redirect URL.

The source codes are available [here](https://github.com/SonQBChau/keycloak-setup)
