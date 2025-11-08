# 🐳 Install Docker Engine on Ubuntu

---

## **1. Uninstall Old Versions**

Run the following command to remove any old or conflicting Docker packages:

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do \
  sudo apt-get remove $pkg; \
  done
```

---

## **2. Set Up the Docker Apt Repository**

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl -y
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
```

---

## **3. Install Docker Engine**

Install the latest version of Docker Engine, CLI, and related components:

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

---

## **4. Start and Enable Docker**

Check if Docker is running:

```bash
sudo systemctl status docker
```

If it’s not running, start Docker manually:

```bash
sudo systemctl start docker
```

Enable Docker to start automatically on boot:

```bash
sudo systemctl enable docker
```

---

## **5. Verify the Installation**

Run the hello-world image to confirm Docker is installed correctly:

```bash
sudo docker run hello-world
```

If successful, you’ll see a confirmation message indicating Docker is working properly.

---

## **6. Manage Docker as a Non-Root User**

Create a Docker group and add your user to it:

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

Apply the group changes:

```bash
newgrp docker
```

Verify you can run Docker without sudo:

```bash
docker run hello-world
```

---

✅ **Docker Engine is now successfully installed and configured on your Ubuntu system.**

