# Wordpress Docker Compose Set up

This project provides a ready-to-use Docker Compose setup to run WordPress with MariaDB, Redis, and phpMyAdmin. It's ideal for local development, testing, or quick prototyping.

## Services Included

- **WordPress**: The popular CMS, running on the official image.
- **MariaDB**: MySQL-compatible database for WordPress.
- **Redis**: In-memory cache, can be used to improve WordPress performance.
- **phpMyAdmin**: Web interface for database management.

---

## Prerequisites

### 1. Install Docker Engine

Docker Engine is required to run containers on your machine.

#### **Install on Ubuntu/Linux**

```bash
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### **Install on Windows/Mac**

- Download and install Docker Desktop from [Docker's official site](https://www.docker.com/products/docker-desktop/).

#### **Verify Installation**

```bash
docker --version
docker compose version
```

---

## Getting Started

## 1. Create a Project Directory 

```bash
mkdir DockerWorpress

cd DockerWordpress

ls
```

### 2. Clone the Repository

```bash
git clone https://github.com/ttdickson86/OllamaDockerWordpress.git
cd OllamaDockerWordpress
```

### 3. Start the Services

```bash
docker compose up -d
```

This command will start all services in the background.

---

## Access the Applications

- **WordPress**: [http://localhost:9080](http://localhost:9080)
- **phpMyAdmin**: [http://localhost:8080](http://localhost:8080)
  - Server: `db`
  - Username: `root` or `wordpress`
  - Password: `your_password` (as set in `docker-compose.yaml`)

---

## Stopping the Stack

```bash
docker compose down
```

---

## Configuration

You can change database credentials and other settings in the `docker-compose.yaml` file as needed.

---

## Notes

- **Passwords**: The default password is `your_password`. For production use, change this to a strong, unique password.
- **Data Persistence**: This setup does **not** include persistent volumes. All data will be lost if containers are removed. For persistent storage, add Docker volumes to the services.
- **Redis**: WordPress needs a plugin to use Redis for object caching.

---

## Troubleshooting

- Make sure Docker Engine is running before starting the services.
- If ports are already in use, edit the `docker-compose.yaml` to change them.

---

## License

MIT
