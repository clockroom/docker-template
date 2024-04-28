# SSL reverse proxy with self-signed certificate

## Get started

1. Issue a Root CA certificate
    ```sh
    docker compose -f docker-compose-issue.yml build
    ```

2. Issue a server certificate and build an SSL reverse proxy
    ```sh
    docker compose up -d
    ```

3. Export the server certificate from the SSL reverse proxy
    ```sh
    docker compose exec proxy cp /etc/nginx/ssl/ca.crt /app/
    ```
    The Root CA certificate named "ca.crt" is copied to the bind mount directory.
    Install "ca.crt" into your OS (for Chrome, Safari, etc.) or browser (for Firefox, etc.).
