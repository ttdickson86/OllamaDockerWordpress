# WordPress with UpdraftPlus + Docker Compose

This setup builds a custom WordPress container with the latest WordPress image and the UpdraftPlus backup plugin pre-installed.

## Prerequisites

- **Docker Engine** must be installed on your system.  
  [Docker Install Instructions](https://docs.docker.com/engine/install/)

## Setup Steps

1. **Clone this repository**  
   ```sh
   git clone https://github.com/ttdickson86/OllamaDockerWordpress.git
   cd OllamaDockerWordpress
   ```

2. **Build and Start the Containers**  
   ```sh
   docker compose up --build
   ```

3. **Access Your Services**
   - WordPress: [http://localhost:9080](http://localhost:9080)
   - phpMyAdmin: [http://localhost:8080](http://localhost:8080)

4. **Login to WordPress**
   - On first launch, set up your admin account.
   - Go to *Plugins* > *Installed Plugins*. UpdraftPlus will be pre-installed and activated.

5. **Configure UpdraftPlus**
   - In the WordPress admin, go to *Settings* > *UpdraftPlus Backups*.
   - Set up remote storage and configure backups as desired.

## Customization

- The WordPress Dockerfile is located at `wordpress/Dockerfile`.
- To add more plugins, modify the Dockerfile and rebuild (`docker-compose build wordpress`).

## Notes

- Default database credentials are in `docker-compose.yaml`. Change these for production use.
- This setup includes Redis for caching and phpMyAdmin for database management.

## Stopping the Containers

```sh
docker-compose down
```

## Troubleshooting

- If you see plugin install errors, check the Docker build logs.
- Ensure Docker Engine is running before executing any commands.
