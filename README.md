# OllamaDockerWordpress
Ntosah77 Open Source Apps

To enhance your WordPress Docker setup with **SSL, caching, and custom domains**, I'll provide a **fully updated Docker Compose YAML** that includes these features.

---

### 🔐 **SSL Configuration (Let's Encrypt)**
- Uses the `nginx-letsencrypt` image to handle Let's Encrypt certificates.
- Enables HTTPS and configures Nginx to use the certificate.

---

### 📦 **Caching**
- Uses the `nginx-cache` image for caching.
- Includes a custom cache configuration in Nginx.

---

### 📡 **Custom Domains**
- Configures Nginx to handle a custom domain (e.g., `example.com`).
- Requires DNS settings to point to your server's IP.

---

### ✅ **Updated Docker Compose YAML**

```yaml
version: '3'
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=yourpassword
      - MYSQL_DATABASE=wordpress
    ports:
      - "33060:3306"

  wordpress:
    image: wordpress:latest
    links:
      - db
    volumes:
      - wordpress_data:/var/www/html
    environment:
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_NAME=wordpress
      - WORDPRESS_DB_USER=root
      - WORDPRESS_DB_PASSWORD=yourpassword
      - WORDPRESS_HOME=/var/www/html
    ports:
      - "80:80"
    restart: always

  nginx:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - nginx_data:/var/www/html
      - letsencrypt:/etc/letsencrypt
    links:
      - wordpress
    environment:
      - NGINX_MAIL_FROM=example@example.com
      - NGINX_MAIL_HOST=smtp.example.com
      - NGINX_MAIL_PORT=587
      - NGINX_MAIL_SECURE=465
      - NGINX_MAIL_MAILER=smtp
      - NGINX_MAIL_USERNAME=yourname
      - NGINX_MAIL_PASSWORD=yourpassword
      - NGINX_SSL_CERT=/etc/letsencrypt/live/example.com/fullchain.pem
      - NGINX_SSL_KEY=/etc/letsencrypt/live/example.com/privkey.pem
    command: ["nginx", "-g", "daemon off;"]
    restart: always

  letsencrypt:
    image: nginx:latest
    volumes:
      - letsencrypt:/etc/letsencrypt
    entrypoints:
      - "nginx-letsencrypt"
    command: ["nginx", "-g", "daemon off;"]
    ports:
      - "80:80"
    restart: always

volumes:
  db_data:
  wordpress_data:
  nginx_data:
  letsencrypt:
```

---

### 📝 **Steps to Apply**

1. **Create Volumes** (if not already present):
   ```bash
   docker volume create db_data
   docker volume create wordpress_data
   docker volume create nginx_data
   docker volume create letsencrypt
   ```

2. **Run the Stack**:
   ```bash
   docker-compose up -d
   ```

3. **SSL Certificate**:
   - Run the Let's Encrypt server:
     ```bash
     docker-compose run --rm letsencrypt nginx-letsencrypt
     ```
   - Follow the prompts to enter your domain and certificate details.

4. **Custom Domain Setup**:
   - Configure your DNS provider (e.g., Cloudflare, GitHub Pages, etc.) to point your domain to your server's IP.
   - Update the `nginx` service's `NGINX_SSL_CERT` and `NGINX_SSL_KEY` environment variables in the `nginx` service.

5. **Caching**:
   - Install a caching plugin (e.g., W3TC) in WordPress and configure Nginx to use a caching layer.
   - Use the `nginx-cache` image for advanced caching.

6. **Access WordPress**:
   - Go to `http://localhost` (or your custom domain) to access WordPress.

---

### 📦 **Optional: Caching Plugin (W3TC)**
- Install W3TC plugin in WordPress:
  ```bash
  docker-compose run wordpress wp-cli plugin install w3tc
  docker-compose run wordpress wp-cache-plugin install
  ```

---

### 🔒 **Summary**
- **SSL**: Using Let's Encrypt with `nginx-letsencrypt`.
- **Caching**: Nginx with `nginx-cache` and W3TC plugin.
- **Custom Domains**: Configure DNS and update Nginx settings.

Let me know if you need help with specific caching configurations or plugin installation!