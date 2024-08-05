---
layout: ../../layouts/BlogLayout.astro
title: 'How use Vscode debugpy inside a running container'
published: 'Aug 5 2024'
tags: [vscode]
---

## How to Use VS Code Debugpy Inside a Running Container

If you’re working on a Docker project with multiple containers and want to set up debugger inside one of them using Vscode, here’s a simple guide to help you get started.

## Step 1: Use a Pre-Configured Template

Start by using the template from [FastAPI Full-Stack Template](https://github.com/fastapi/full-stack-fastapi-template).

## Step 2: Expose the Debugging Port

Modify your `docker-compose.override.yml` file to expose port 5678 for debugging:

```yaml
backend:
  restart: "no"
  ports:
    - "8888:8888"
    - "5678:5678" # new

```

## Step 3: Install Debugpy

Since the template uses Poetry for dependency management, add Debugpy to your project with the following command:

```bash
poetry install debugpy
```

## Step 4: Configure VS Code

Create a `launch.json` file in the `.vscode` directory with the following configuration:

```json
{
  "name": "debugpy",
  "type": "debugpy",
  "request": "attach",
  "justMyCode": false,
  "pathMappings": [
    {
      "localRoot": "${workspaceFolder}/backend/app",
      "remoteRoot": "/app/app"
    }
  ],
  "connect": {
    "port": 5678,
    "host": "localhost"
  }
}
```

In this configuration:

- `localRoot` is the path where your code is located locally.
- `remoteRoot` is where the code is copied inside the container.

## Step 5: Add Debugpy to Your Python Entrypoint

Modify your Python entrypoint (e.g., `backend/app/api/main.py`) to include Debugpy:

```python
import debugpy

debugpy.log_to("logs")
debugpy.configure(python="/usr/local/bin/python")
debugpy.listen(("0.0.0.0", 5678))
print("⏳ VS Code debugger can now be attached, press F5 in VS Code ⏳")
debugpy.wait_for_client()
print("🎉 VS Code debugger attached, enjoy debugging 🎉")

# existing code
api_router = APIRouter()
...
```

This will allow VS Code to attach to the debugger when you start debugging.

## Step 6: Rebuild and Start Your Container

Rebuild your Docker container with the following command:

```bash
docker compose up -d --build
```

After rebuilding, the backend container should pause at the message:

```
⏳ VS Code debugger can now be attached, press F5 in VS Code ⏳
```

## Step 7: Start Debugging

In VS Code, choose the `debugpy` configuration and click "Debug". Inside the container, you should see:

```
🎉 VS Code debugger attached, enjoy debugging 🎉
```

That's it! You can now debug your FastAPI project running inside
