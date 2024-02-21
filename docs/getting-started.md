---
sidebar_position: 2
title: "🔑 Getting Started"
---

## How to Install 🚀

🌟 **Important Note on User Roles and Privacy:**

- **Admin Creation:** The very first account to sign up on Open WebUI will be granted **Administrator privileges**. This account will have comprehensive control over the platform, including user management and system settings.

- **User Registrations:** All subsequent users signing up will initially have their accounts set to **Pending** status by default. These accounts will require approval from the Administrator to gain access to the platform functionalities.

- **Privacy and Data Security:** We prioritize your privacy and data security above all. Please be reassured that all data entered into Open WebUI is stored locally on your device. Our system is designed to be privacy-first, ensuring that no external requests are made, and your data does not leave your local environment. We are committed to maintaining the highest standards of data privacy and security, ensuring that your information remains confidential and under your control.

### Steps to Install Open WebUI

#### Before You Begin

1. **Installing Docker:**

   - **For Windows and Mac Users:**

     - Download Docker Desktop from [Docker's official website](https://www.docker.com/products/docker-desktop).
     - Follow the installation instructions provided on the website. After installation, open Docker Desktop to ensure it's running properly.

   - **For Ubuntu and Other Linux Users:**
     - Open your terminal.
     - Set up your Docker apt repository according to the [Docker documentation](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
     - Update your package index:
       ```bash
       sudo apt-get update
       ```
     - Install Docker using the following command:
       ```bash
       sudo apt-get install docker-ce docker-ce-cli containerd.io
       ```
     - Verify the Docker installation with:
       ```bash
       sudo docker run hello-world
       ```
       This command downloads a test image and runs it in a container, which prints an informational message.

2. **Ensure You Have the Latest Version of Ollama:**

   - Download the latest version from [https://ollama.com/](https://ollama.com/).

3. **Verify Ollama Installation:**
   - After installing Ollama, check if it's working by visiting [http://127.0.0.1:11434/](http://127.0.0.1:11434/) in your web browser. Remember, the port number might be different for you.

#### Installing with Docker 🐳

- **Important:** When using Docker to install Open WebUI, make sure to include the `-v open-webui:/app/backend/data` in your Docker command. This step is crucial as it ensures your database is properly mounted and prevents any loss of data.

- **If Ollama is on your computer**, use this command:

  ```bash
  docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
  ```

- **To build the container yourself**, follow these steps:

  ```bash
  docker build -t open-webui .
  docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always open-webui
  ```

- After installation, you can access Open WebUI at [http://localhost:3000](http://localhost:3000).

#### Using Ollama on a Different Server

- To connect to Ollama on another server, change the `OLLAMA_API_BASE_URL` to the server's URL:

  ```bash
  docker run -d -p 3000:8080 -e OLLAMA_API_BASE_URL=https://example.com/api -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
  ```

  Or for a self-built container:

  ```bash
  docker build -t open-webui .
  docker run -d -p 3000:8080 -e OLLAMA_API_BASE_URL=https://example.com/api -v open-webui:/app/backend/data --name open-webui --restart always open-webui
  ```

### Installing Ollama and Open WebUI Together

#### Using Docker Compose

- If you don't have Ollama yet, use Docker Compose for easy installation. Run this command:

  ```bash
  docker compose up -d --build
  ```

- **For GPU Support:** Use an additional Docker Compose file:

  ```bash
  docker compose -f docker-compose.yaml -f docker-compose.gpu.yaml up -d --build
  ```

- **To Expose Ollama API:** Use another Docker Compose file:

  ```bash
  docker compose -f docker-compose.yaml -f docker-compose.api.yaml up -d --build
  ```

#### Using `run-compose.sh` Script (Linux or Docker-Enabled WSL2 on Windows)

- Give execute permission to the script:

  ```bash
  chmod +x run-compose.sh
  ```

- For CPU-only container:

  ```bash
  ./run-compose.sh
  ```

- For GPU support (read the note about GPU compatibility):

  ```bash
  ./run-compose.sh --enable-gpu
  ```

- To build the latest local version, add `--build`:

  ```bash
  ./run-compose.sh --enable-gpu --build
  ```

### Alternative Installation Methods

For other ways to install, like using Kustomize or Helm, check out [INSTALLATION.md](/INSTALLATION.md). Join our [Open WebUI Discord community](https://discord.gg/5rJgQTnV4s) for more help and information.

### Updating your Docker Installation

In case you want to update your local Docker installation to the latest version, you can do it performing the following actions:

```bash
docker rm -f open-webui
docker pull ghcr.io/open-webui/open-webui:main
[insert command you used to install]
```

In the last line, you need to use the very same command you used to install (local install, remote server, etc.)