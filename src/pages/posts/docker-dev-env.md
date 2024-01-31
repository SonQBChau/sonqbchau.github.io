---
layout: ../../layouts/BlogLayout.astro
title: Simplify Your Development Workflow with Dev Environments
tags: [python, web, django]
published: 'July 05 2023'
description: 'Lorem ipsum dolor sit amet'

---

## Introduction

In this blog post, we will explore how Dev Environments can simplify development and streamline the process of creating, running, and sharing code.

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img src="https://github.com/SonQBChau/sonqbchau.github.io/assets/12553570/9605724e-83c2-4a1f-a630-8166047af76e"
  alt="Docker Dev Environments"
  width="95%" style="margin: 10px 10px 10px 10px;">
 <figcaption>Figure 1: Docker Dev Environments.</figcaption>
</figure>

### Development with Docker: The Challenges

Developing applications using Docker can be challenging, especially when it comes to certain aspects of the development workflow. Here are some common pain points faced by developers:

1. **Setting up the Debugger:**
   Configuring the debugger to work seamlessly with a Dockerized application can be complicated, especially with a complex stack, where multiple services need to run simultaneously. Running a single service for debugging might not be enough to trace errors effectively.

2. **Slow Testing:**
   Reviewing pull requests or making changes can be time-consuming, as it often involves rebuilding the entire container or stack. This disrupts the current working environment when switching between branches or features. Developers need a faster and more efficient approach to test changes without compromising productivity.

3. **Development is Not the Same as Deployment:**
   The development environment often differs from the production environment in various aspects, such as running in debug mode or including specific packages for testing and monitoring dependencies. Customizing the Docker environment manually for specific requirements becomes repetitive when frequently switching between different containers. Developers need a flexible and customizable approach to create their own environments.

### Introducing Docker Dev Environments

To address these challenges, Docker introduced a new feature called Dev Environments to simplify the development workflow by providing quick and configurable environments with pre-configured code and tools. Developers can leverage an intuitive GUI to effortlessly launch and manage these containers, reducing the time spent on manual setup and enabling a seamless development experience.

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img src="https://github.com/SonQBChau/sonqbchau.github.io/assets/12553570/89fd141b-3678-4387-a8e1-888e16d1e773"
  alt="Docker Dev Environments Interface"
  width="95%" style="margin: 10px 10px 10px 10px;">
 <figcaption>Figure 2: Docker Dev Environments Interface</figcaption>
</figure>

Let's take a closer look at how it works:

1. **Setup Dev Environment:**
   Define your development environment with the necessary services and configurations by creating a `compose-dev.yaml` file.

2. **Running Dev Environment:**
   - Select the Git repository of your project.
   - Choose your preferred Integrated Development Environment (IDE) that supports Docker.
   - Open your terminal and run the command `make run`. This will launch your application and provide you with a development-ready environment.

3. **Sharing Dev Environment:**
   Generate a link using the URL `https://open.docker.com/dashboard/dev-envs?url=` followed by the repository link and share it with your team members, allowing them to access the same development environment.

### How to Use Docker for Development

You can start by choosing an [example](https://github.com/docker/awesome-compose) that suits your needs. For this guide, we will use the [react-express-mysql](https://github.com/docker/awesome-compose/tree/master/react-express-mysql).

After selecting the example, set up your development environment:

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img src="https://github.com/SonQBChau/sonqbchau.github.io/assets/12553570/8c959c31-405c-4203-8a85-16edb3074a78"
  alt="Opening the Project in VSCode"
  width="95%" style="margin: 10px 10px 10px 10px;">
 <figcaption>Figure 3: Opening the Project in VSCode</figcaption>
</figure>

1. Open the project in Visual Studio Code (VSCode).

2. Navigate to the "frontend" folder using the terminal/command prompt: `cd frontend`.

3. Install the required dependencies: `npm install`.

4. Start the frontend development server: `npm start`.

Now, your frontend is running in development mode. You can make any changes to the code and use `git commit` or `git pull` without needing to rebuild the Docker container or the entire stack.

### Collaboration with Teammates

If your teammate makes changes to the backend and asks you to review them, you can set up another development environment without affecting your current one.

### Debugging

1. To debug issues in the frontend, you already have the development environment running from Step 4.

2. For backend debugging, switch your dev environment:
   - Make the "backend" folder your working directory: `cd backend`.
   - Install any necessary debugger (e.g., the default built-in JavaScript debugger in VSCode).
   - Install the required dependencies: `npm install`.
   - Start the backend server with the debugger: `npm start`.
   - Set breakpoints or use the debugger as needed to investigate issues.

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img src="https://github.com/SonQBChau/sonqbchau.github.io/assets/12553570/9310f11b-facd-434d-b686-6d2ab62de1df"
  alt="Debugging the Backend with VSCode"
  width="95%" style="margin: 10px 10px 10px 10px;">
 <figcaption>Figure 4: Debugging the Backend with VSCode</figcaption>
</figure>

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img src="https://github.com/SonQBChau/sonqbchau.github.io/assets/12553570/ea6a5630-d35d-4271-99ae-7d1cd14e2099"
  alt="Setting a Breakpoint for Investigation"
  width="95%" style="margin: 10px 10px 10px 10px;">
 <figcaption>Figure 5: Setting a Breakpoint for Investigation</figcaption>
</figure>

Once you're done with debugging, you can shut down the backend environment and return to working on the frontend.

### Conclusion

Docker Dev Environments can speed up development with seamless integration and debugging capabilities with IDEs. Additionally, Docker Dev Environments simplify the setup and distribution of development environments, allowing for effortless collaboration and sharing. By leveraging Docker Dev Environments, developers can optimize their workflow, enhance efficiency, and increase productivity.
