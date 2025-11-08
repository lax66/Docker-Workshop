# Building Images, Tagging, Publishing, and Using Build Cache

## Building Images

1. Building images is the process of building an image based on a Dockerfile.

2. Most often, images are built using a Dockerfile.

3. The most basic docker build command might look like the following:

   ```bash
   docker build .
   ```

4. The final `.` in the command provides the path or URL to the build context.

5. At this location, the builder will find the Dockerfile and other referenced files.

6. When you run a build, the builder pulls the base image, if needed, and then runs the instructions specified in the Dockerfile.

7. With the previous command, the image will have no name, but the output will provide the ID of the image.

### Example Output

```bash
docker build .
[+] Building 3.5s (11/11) FINISHED
 => [internal] load build definition from Dockerfile        0.0s
 => [internal] load metadata for docker.io/library/python:3.12
 => [internal] load .dockerignore                           0.0s
 => => transferring context: 2B                             0.0s
 ...
```

8. With the previous output, you could start a container by using the referenced image:

   ```bash
   docker run sha256:9924dfd9350407b3df01d1a0e1033b1e543523ce7d5d5e2c83a724480ebe8f00
   ```

9. That name certainly isn't memorable, which is where tagging becomes useful.

---

## Tagging Images

1. Tagging images is the method to provide an image with a memorable name.
2. However, there is a structure to the name of an image.
3. A full image name has the following structure:

   ```
   [HOST[:PORT_NUMBER]/]PATH[:TAG]
   ```

### Components

* **HOST:** The optional registry hostname where the image is located. If no host is specified, Docker's public registry at docker.io is used by default.
* **PORT_NUMBER:** The registry port number if a hostname is provided.
* **PATH:** The path of the image, consisting of slash-separated components. For Docker Hub, the format follows `[NAMESPACE/]REPOSITORY`, where namespace is either a user's or organization's name. If no namespace is specified, library is used, which is the namespace for Docker Official Images.
* **TAG:** A custom, human-readable identifier that's typically used to identify different versions or variants of an image. If no tag is specified, latest is used by default.

### Examples of Image Names

* `nginx`, equivalent to `docker.io/library/nginx:latest`
* `docker/welcome-to-docker`, equivalent to `docker.io/docker/welcome-to-docker:latest`

### Tag During Build

```bash
docker build -t my-username/my-image .
```

### Add Another Tag

```bash
docker image tag my-username/my-image another-username/another-image:v1
```

---

## Publishing Images

1. Once you have an image built and tagged, you're ready to push it to a registry.

2. To do so, use the docker push command:

   ```bash
   docker push my-username/my-image
   ```

3. Within a few seconds, all of the layers for your image will be pushed to the registry.

### Requiring Authentication

* Before you're able to push an image to a repository, you will need to be authenticated.
* To do so, simply use the docker login command.

  ```bash
  docker login
  ```

---

## LAB: Build, Tag, and Publish an Image

* Use the previous dockerfile (Day5) to build, tag and publish it in dockerhub.

---

## Using the Build Cache

### Example Dockerfile

```dockerfile
FROM node:22-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "./src/index.js"]
```

---

## How Docker Build Cache Works

1. When you run docker build, Docker follows your Dockerfile step-by-step, and for each instruction it creates a layer.
2. To speed up future builds, Docker remembers these layers. This is called the build cache.
3. If Docker sees that a step hasn’t changed since the last build, it reuses the cached layer instead of rebuilding it.
4. This makes the build much faster and saves time and resources.

---

## When Does Cache Break

1. Cache gets invalidated when Docker detects a change.
2. If a layer is invalidated, all layers after that must rebuild.
3. Cache breaks when:

   * RUN instruction changes.
   * Files used in COPY or ADD change (content or permissions).
   * Any earlier layer changes.
4. If one layer is rebuilt, all layers below it must also rebuild.

---

## Why This Matters

1. Using the cache correctly means faster builds.
2. Avoiding unnecessary changes to early steps helps keep later layers cached.
3. Proper Dockerfile structure can save a lot of build time.

---

## LAB: Using the Build Cache

* Link: [https://github.com/dockersamples/todo-list-app](https://github.com/dockersamples/todo-list-app)
---

# LAB: Build, Tag, and Publish an Image

### Building Images

1. Building images is the process of creating a Docker image based on a Dockerfile.

2. Most often, images are built using a Dockerfile.

3. Use the following command to build an image. Replace `YOUR_DOCKER_USERNAME` with your actual Docker Hub username:

   ```bash
   docker build -t YOUR_DOCKER_USERNAME/concepts-build-image-demo .
   ```

4. Example:

   ```bash
   docker build -t mobywhale/concepts-build-image-demo .
   ```

5. Once the build is complete, you can view your image with:

   ```bash
   docker image ls
   ```

   Example output:

   ```bash
   REPOSITORY                             TAG       IMAGE ID       CREATED          SIZE
   mobywhale/concepts-build-image-demo    latest    746c7e06537f   24 seconds ago   354MB
   ```

6. To view the history of how the image was created, use:

   ```bash
   docker image history mobywhale/concepts-build-image-demo
   ```

   Example output:

   ```bash
   IMAGE          CREATED         CREATED BY                                      SIZE      COMMENT
   f279389d5f01   8 seconds ago   CMD ["node" "./src/index.js"]                   0B        buildkit.dockerfile.v0
   <missing>      8 seconds ago   EXPOSE map[3000/tcp:{}]                         0B        buildkit.dockerfile.v0
   <missing>      8 seconds ago   WORKDIR /app                                    8.19kB    buildkit.dockerfile.v0
   <missing>      4 days ago      /bin/sh -c #(nop)  CMD ["node"]                 0B
   <missing>      4 days ago      /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B
   <missing>      4 days ago      /bin/sh -c #(nop) COPY file:4d192565a7220e13…   20.5kB
   <missing>      4 days ago      /bin/sh -c apk add --no-cache --virtual .bui…   7.92MB
   <missing>      4 days ago      /bin/sh -c #(nop)  ENV YARN_VERSION=1.22.19     0B
   <missing>      4 days ago      /bin/sh -c addgroup -g 1000 node     && addu…   126MB
   <missing>      4 days ago      /bin/sh -c #(nop)  ENV NODE_VERSION=20.12.0     0B
   <missing>      2 months ago    /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B
   <missing>      2 months ago    /bin/sh -c #(nop) ADD file:d0764a717d1e9d0af…   8.42MB
   ```

   This output shows all the layers of the image, including both your custom layers and the ones inherited from the base image.

---

## Authenticating with Docker Hub Using a Personal Access Token (PAT)

1. Before pushing images to Docker Hub, you must log in using your Docker Hub credentials.

2. It is recommended to use a **Personal Access Token (PAT)** instead of your password for security reasons.

3. Generate a PAT from your Docker Hub account settings under **Security → Access Tokens**.

4. Use the following command to log in:

   ```bash
   docker login -u YOUR_DOCKER_USERNAME
   ```

5. When prompted for a password, paste your **Personal Access Token (PAT)** instead.

   Example:

   ```bash
   Username: mobywhale
   Password: <paste-your-PAT-here>
   Login Succeeded
   ```

---

### Pushing the Image to Docker Hub

1. Once authenticated, push your image to Docker Hub using the following command:

   ```bash
   docker push YOUR_DOCKER_USERNAME/concepts-build-image-demo
   ```

2. Example:

   ```bash
   docker push mobywhale/concepts-build-image-demo
   ```

3. If you receive the following error:

   ```bash
   requested access to the resource is denied
   ```

   Ensure that:

   * You are logged in with the correct Docker Hub account.
   * The image tag contains your correct Docker Hub username.

4. After a short while, your image will be successfully pushed to Docker Hub and visible in your repositories.

---
---
# LAB: Understanding Docker Build Cache

### Step 1: Clone the Sample Application

1. Clone the official sample application repository:

   ```bash
   git clone https://github.com/dockersamples/todo-list-app
   cd todo-list-app
   ```

2. Inside this directory, you’ll find a `Dockerfile` similar to the following:

   ```dockerfile
   FROM node:22-alpine
   WORKDIR /app
   COPY . .
   RUN yarn install --production
   EXPOSE 3000
   CMD ["node", "./src/index.js"]
   ```

---

### Step 2: Build the Image for the First Time

1. Build the image using the following command:

   ```bash
   docker build .
   ```

2. The first build will take longer because Docker downloads the base image and installs all Node.js dependencies.

---

### Step 3: Rebuild Without Any Changes

1. Run the build again without modifying any files:

   ```bash
   docker build .
   ```

2. This time, the build will complete much faster because Docker **reuses cached layers**.

3. Since nothing has changed, Docker skips unnecessary steps like dependency installation.

4. In short: if the **Dockerfile** and **build context** remain unchanged, Docker leverages its cache to speed up the build process.

---

### Step 4: Understanding Cache Invalidation

1. If any file in the project changes — even a simple HTML file — the cache for the `COPY . .` step becomes invalid.
2. When that happens, Docker must re-run all subsequent steps, including dependency installation.
3. This can be inefficient for large projects.
4. To avoid this, we restructure the Dockerfile so dependency installation only occurs when necessary.
5. For Node.js projects, dependencies are defined in the `package.json` file, and changes to this file should trigger dependency installation.

---

### Step 5: Optimize the Dockerfile for Better Caching

1. Modify the Dockerfile as shown below:

   ```dockerfile
   FROM node:22-alpine
   WORKDIR /app
   COPY package.json yarn.lock ./
   RUN yarn install --production
   COPY . .
   EXPOSE 3000
   CMD ["node", "src/index.js"]
   ```

2. When you run `yarn install`, Yarn automatically generates or updates a **`yarn.lock`** file.

3. This file locks down the exact versions of dependencies and sub-dependencies installed.

4. This structure ensures:

   * Dependencies install **only when `package.json` or `yarn.lock` changes**.
   * Code updates do **not trigger dependency installation** again.

---

### Step 6: Using `.dockerignore`

1. When Docker builds an image, it sends all files from your project to the Docker daemon — known as the **build context**.

2. Large or unnecessary directories (e.g., `node_modules`, logs, or temporary files) increase build time and image size.

3. A `.dockerignore` file helps exclude these files from the build context.

4. It works like a `.gitignore` file but specifically for Docker.

5. Create a `.dockerignore` file in your project root and add the following:

   ```bash
   node_modules
   ```

6. This ensures Docker ignores the `node_modules` folder during builds, improving performance and preventing redundant data from being copied into the image.

---

### Step 7: Build the Optimized Image

1. Run the following command to build your optimized image:

   ```bash
   docker build -t node-app:2.0 .
   ```

2. Since the Dockerfile has changed, all layers will rebuild — this is expected.

---

### Step 8: Make a Small Code Change and Rebuild

1. Modify the file `src/static/index.html` (for example, update the title to “The Awesome Todo App”).

2. Build the image again:

   ```bash
   docker build -t node-app:3.0 .
   ```

3. Observe the build process:

   * ✅ Dependency installation step is **cached**.
   * ✅ The build is significantly faster.
   * ✅ Only the modified steps run again.

4. This demonstrates the true **power and efficiency of Docker build c



