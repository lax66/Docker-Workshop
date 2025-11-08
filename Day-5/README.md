# 🧱 Building Images — Dockerfile Explanation

---

## **What is a Dockerfile?**

* A **Dockerfile** is a text-based document used to **create a container image**.
* It provides **instructions** for the image builder — defining commands to run, files to copy, environment variables, startup commands, and more.
* A Dockerfile has **no file extension**. Some text editors may warn or try to add one — ignore that.

### **Dockerfile Reference**

Docker builds images automatically by reading instructions from a Dockerfile.
It contains all the commands a user could execute manually in the terminal to assemble an image.

**Format of a Dockerfile:**

```dockerfile
# Comment
INSTRUCTION arguments
```

* The instruction names are **not case-sensitive**, but by convention, they’re written in **UPPERCASE**.
* Docker executes the instructions **in order**.
* A Dockerfile must begin with a **FROM** instruction (after optional comments or parser directives).

---

## **Parser Directives in a Dockerfile**

Parser directives are special instructions placed at the **top of a Dockerfile**.
They define how Docker should interpret the file before executing the build instructions.

* They always start with a `#` followed by a recognized key (like `syntax=` or `escape=`).
* Think of them as **settings for the Dockerfile**, not commands.

### **Common Parser Directives**

#### **1. syntax=**

Specifies which **syntax or builder version** Docker should use.

**Example:**

```dockerfile
# syntax=docker/dockerfile:1.5
FROM python:3.13
```

* Useful when using advanced BuildKit features (caching, mounts, secrets, etc.).
* Ensures compatibility with new Dockerfile syntax.

#### **2. escape=**

Defines the **escape character** used for line continuations.

**Example (Windows):**

```dockerfile
# escape=`
FROM mcr.microsoft.com/windows/servercore:ltsc2022
RUN powershell -Command Write-Host "Hello"
```

* Default escape character: `\` (Linux/Mac)
* Optional escape character: `` ` `` (Windows)

**Important:**

* Parser directives must appear **before any non-comment instruction** like `FROM`.
* They **don’t become part of the image** — they only affect how Docker reads the file.

---

## **Example Dockerfile — Python Application**

```dockerfile
FROM python:3.13
WORKDIR /usr/local/app

# Install the application dependencies
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Copy the source code
COPY src ./src
EXPOSE 8080

# Create a non-root user for running the app
RUN useradd app
USER app

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8080"]
```

---

## **Common Dockerfile Instructions**

| Instruction                     | Description                                                   |
| ------------------------------- | ------------------------------------------------------------- |
| **FROM <image>**                | Specifies the base image to build from.                       |
| **WORKDIR <path>**              | Sets the working directory inside the image.                  |
| **COPY <src> <dest>**           | Copies files from host to the image.                          |
| **RUN <command>**               | Executes a command while building the image.                  |
| **ENV <name> <value>**          | Sets environment variables.                                   |
| **EXPOSE <port>**               | Documents the port the container will listen on.              |
| **USER <user-or-uid>**          | Sets the default user for subsequent instructions.            |
| **CMD ["<command>", "<arg1>"]** | Defines the default command to run when the container starts. |

---

## **Full Dockerfile Instruction Reference**

| Instruction     | Description                                     |
| --------------- | ----------------------------------------------- |
| **ADD**         | Add local or remote files and directories.      |
| **ARG**         | Define build-time variables.                    |
| **CMD**         | Specify default commands.                       |
| **COPY**        | Copy files and directories.                     |
| **ENTRYPOINT**  | Define the default executable.                  |
| **ENV**         | Set environment variables.                      |
| **EXPOSE**      | Describe which ports your app listens on.       |
| **FROM**        | Create a new build stage from a base image.     |
| **HEALTHCHECK** | Check a container’s health at startup.          |
| **LABEL**       | Add metadata to an image.                       |
| **MAINTAINER**  | Specify the author of the image.                |
| **ONBUILD**     | Define instructions for child images.           |
| **RUN**         | Execute build commands.                         |
| **SHELL**       | Set the default shell.                          |
| **STOPSIGNAL**  | Define the system signal to stop the container. |
| **USER**        | Set user and group ID.                          |
| **VOLUME**      | Create volume mounts.                           |
| **WORKDIR**     | Change the working directory.                   |

---

## **Custom Dockerfile Names and Usage**

By default, Docker looks for a file named **Dockerfile** (capital D, no extension) in the current directory when you run:

```bash
docker build .
```

Sometimes, you might use **custom Dockerfile names** for different environments (e.g., development, production, testing):

* `Dockerfile.dev`
* `Dockerfile.prod`
* `Dockerfile.test`

Use the **-f** flag to specify a custom Dockerfile:

```bash
docker build -f Dockerfile.dev -t myapp:dev .
```

### **Explanation:**

* `-f Dockerfile.dev` → specifies the Dockerfile name.
* `-t myapp:dev` → tags the image.
* `.` → specifies the build context (directory used during build).

---

## **LAB: Write a Dockerfile for a Simple Node.js Application**

🧠 **Task:**
Write a Dockerfile that builds a simple Node.js app using this repo:

🔗 [https://github.com/docker/getting-started-todo-app](https://github.com/docker/getting-started-todo-app)

---


