# 🐳 Understanding Docker

---

## **Contents**

1. What is Docker?
2. The Docker Platform
3. What can I use Docker for?
4. Docker Architecture
5. Docker Objects

---

## **1. What is Docker?**

Docker is an **open platform for developing, shipping, and running applications**.
It enables you to **separate your applications from your infrastructure**, allowing you to deliver software faster and more reliably.

With Docker, you can manage your infrastructure in the same way you manage your applications.
By using Docker’s methodologies for **shipping, testing, and deploying code**, you can significantly reduce the time between writing code and running it in production.

---

## **2. The Docker Platform**

Docker allows you to package and run applications in a **loosely isolated environment** called a container.

### Key Characteristics:

* Containers provide **isolation** and **security**, allowing multiple containers to run simultaneously on a single host.
* Containers are **lightweight** and include everything needed to run an application — you don’t need to depend on what’s installed on the host.
* You can **share containers** with others, ensuring consistent behavior across environments.

### Docker Platform Lifecycle:

1. **Develop** your application and supporting components using containers.
2. The **container** becomes the unit for distributing and testing your application.
3. **Deploy** the containerized application into production — either standalone or orchestrated.

   * Works the same on **local data centers**, **cloud**, or **hybrid** environments.

---

## **3. What Can I Use Docker For?**

### **Fast, Consistent Delivery of Applications**

Docker simplifies the development lifecycle by allowing developers to work in standardized environments using **local containers**.
These containers support **CI/CD (Continuous Integration and Continuous Delivery)** workflows.

#### Example Scenario:

1. Developers write code locally and share it via Docker containers.
2. When bugs are found, they fix them and redeploy containers for testing.
3. Docker pushes applications to test environments for automated and manual testing.
4. Once validated, the updated image is pushed to production — simple and consistent.

### **Responsive Deployment and Scaling**

* Docker’s container-based platform allows **highly portable workloads**.
* Containers can run on a **developer’s laptop**, **VMs**, **cloud**, or a **hybrid** environment.
* Because containers are lightweight, you can easily **scale up or down** in near real-time based on business needs.

### **Running More Workloads on the Same Hardware**

* Docker is lightweight and fast, providing a **cost-effective alternative** to VMs.
* This enables you to run **more workloads on the same hardware** and use resources efficiently.
* Ideal for **high-density** or **small-scale** deployments that need better resource utilization.

---

## **4. Docker Architecture**

Docker uses a **client-server architecture**.

* The **Docker Client** communicates with the **Docker Daemon**, which performs heavy tasks like building, running, and distributing containers.
* The client and daemon can run on the **same host** or **different systems**.
* They communicate through a **REST API**, over UNIX sockets or a network interface.
* **Docker Compose** is another client that lets you manage multi-container applications.

### **The Docker Daemon**

* The daemon (`dockerd`) listens for Docker API requests.
* It manages Docker objects — **images**, **containers**, **networks**, and **volumes**.
* It can also communicate with other daemons to manage **Docker services**.

### **The Docker Client**

* The client (`docker`) is the main way users interact with Docker.
* When you run commands like `docker run`, the client sends them to the daemon for execution.
* The Docker client can interact with **multiple daemons**.

### **Docker Desktop**

* Docker Desktop is an easy-to-install application for **Windows**, **macOS**, and **Linux**.
* It includes:

  * Docker Daemon (`dockerd`)
  * Docker Client (`docker`)
  * Docker Compose
  * Docker Content Trust
  * Kubernetes
  * Credential Helper
* It allows you to **build and share containerized applications and microservices** easily.

### **Docker Registries**

* A **Docker registry** stores Docker images.
* **Docker Hub** is the default public registry.
* You can also set up your **own private registry**.

#### Example Commands:

* `docker pull <image>` → Downloads an image from the registry.
* `docker run <image>` → Pulls the image if not available locally and runs it.
* `docker push <image>` → Uploads your image to the configured registry.

---

## **5. Docker Objects**

When using Docker, you work with various **objects**, such as:

* **Images**
* **Containers**
* **Networks**
* **Volumes**
* **Plugins**

### **Images**

* An **image** is a read-only template containing instructions for creating a container.
* Images are often based on other images with custom layers added.
* Example: an image based on `ubuntu` but includes Apache and your web app.

#### Image Creation:

* You create images using a **Dockerfile** — a text file with instructions.
* Each instruction adds a **layer** to the image.
* When you rebuild, only changed layers are re-created, making Docker images **lightweight** and **fast**.

### **Containers**

* A **container** is a runnable instance of an image.
* You can **create**, **start**, **stop**, **move**, or **delete** containers using the Docker CLI or API.
* Containers can be connected to **networks**, have **storage** attached, and even be used to create new images.

#### Container Isolation:

* By default, containers are isolated from each other and the host system.
* You can configure how isolated they are — in terms of **networking**, **storage**, and **permissions**.

#### Persistence:

* When a container is removed, any changes that aren’t saved to persistent storage are lost.

### **Example: Running a Container**

The following command runs an interactive Ubuntu container:

```bash
docker run -i -t ubuntu /bin/bash
```

#### What Happens:

1. Docker checks for the `ubuntu` image locally. If not found, it’s pulled from the registry.
2. A new container is created from the image.
3. Docker allocates a writable filesystem as the final layer.
4. A network interface is created, connecting the container to the default network.
5. `/bin/bash` runs interactively, letting you use the container terminal.
6. When you exit, the container stops but is not deleted — you can start or remove it later.
