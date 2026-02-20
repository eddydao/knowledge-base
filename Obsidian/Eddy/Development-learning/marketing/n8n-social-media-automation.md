# N8N self-host generate social post

# Install n8n with docker

**Step 1: Create a Persistent Volume `docker volume create n8n_data`
Step 2: Run the n8n Container** 

```jsx
docker run -d \
  --name n8n \
  --restart unless-stopped \
  -p 5678:5678 \
  -e TZ=<YOUR_TIMEZONE> \
  -e GENERIC_TIMEZONE=<YOUR_TIMEZONE> \
  -e N8N_BASIC_AUTH_ACTIVE=true \
  -e N8N_BASIC_AUTH_USER=<YOUR_USERNAME> \
  -e N8N_BASIC_AUTH_PASSWORD=<YOUR_PASSWORD> \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n

```

- **Explanations**:
    - **`d`**: Runs in detached (background) mode.
    - **`-name n8n`**: Names the container for easy reference.
    - **`-restart unless-stopped`**: Automatically restarts the container on boot or crashes.
    - **`p 5678:5678`**: Maps port 5678 on your host to the container (access n8n at [**http://localhost:5678**](http://localhost:5678/)).
    - **`e TZ`** and **`e GENERIC_TIMEZONE`**: Sets your timezone for correct scheduling in nodes.
    - **`e N8N_BASIC_AUTH_*`**: Enables basic authentication for security—replace with your desired username and strong password.
    - **`v n8n_data:/home/node/.n8n`**: Mounts the volume to persist data like workflows and encryption keys.

**Step 3: Verify the Installation `docker ps`**

View log: `docker logs n8n`

Step 4: create SSH bridge to port 5678 (default of n8n): `ssh -L 5678:localhost:5678 username@hostname`

# Set up Google Sheet Authen

Create Google Sheets OAuth2 credential: [https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/?utm_source=n8n_app&utm_medium=credential_settings&utm_campaign=create_new_credentials_modal#configure-your-oauth-consent-screen](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/?utm_source=n8n_app&utm_medium=credential_settings&utm_campaign=create_new_credentials_modal#configure-your-oauth-consent-screen)

# Set up custom domain for n8n

## Prerequisites

- n8n installed via Docker (as per our previous discussion).
- A registered domain name (e.g., `yourdomain.com` or a subdomain like `n8n.yourdomain.com`).
- DNS access to point records to your server's public IP.
- Optional: SSL certificate (free via Let's Encrypt) for HTTPS.

## Step 1: Point Your Domain to Your Server's IP

1. Log in to your domain registrar's DNS settings.
2. Create an **A record**:
    - Name/Host: e.g., `n8n` (for `n8n.yourdomain.com`) or `@` (for the root domain).
    - Value: Your server's public IP address (find it with `curl ifconfig.me` on the server).
    - TTL: Default (e.g., 3600 seconds).[n8n+1](https://community.n8n.io/t/an-easy-step-by-step-guide-on-how-to-self-host-n8n/6505)
3. Wait for DNS propagation (5-30 minutes; check with `ping n8n.yourdomain.com` or tools like dnschecker.org).

If using a free subdomain (e.g., from freedns.afraid.org), follow their setup to point it to your IP.youtube

## Step 2: Configure n8n Environment Variables for the Domain

For Docker setups, update your `docker-compose.yml` or `.env` file to set the domain. This ensures internal links, webhooks, and the editor use your custom URL.[hostinger+4](https://www.hostinger.com/support/11927159-changing-the-domain-for-n8n-on-vps-at-hostinger/)

1. SSH into your server (e.g., `ssh user@your_server_ip`).
2. Navigate to your n8n directory (where `docker-compose.yml` is).
3. Stop n8n: `docker compose down`.
4. Edit `.env` (create it if it doesn't exist) or add to `docker-compose.yml` under the `n8n` service's `environment` section:
    
    `textN8N_HOST=n8n.yourdomain.com  # Your custom domain or subdomain
    N8N_PROTOCOL=https           # Use 'http' if no SSL yet
    WEBHOOK_URL=https://n8n.yourdomain.com/  # For webhook endpoints
    N8N_EDITOR_BASE_URL=https://n8n.yourdomain.com/  # For the UI (optional if separating front/back end)
    VUE_APP_URL_BASE_API=https://n8n.yourdomain.com/  # For API base URL`
    
    - If using a specific port, include it (e.g., `https://n8n.yourdomain.com:5678/`), but avoid this for production—use a reverse proxy in Step 3.[n8n+1](https://community.n8n.io/t/how-could-i-use-n8n-editor-base-url/14163)
5. Save and restart: `docker compose up -d`.[helpdesk.gbnetwork+1](https://helpdesk.gbnetwork.com/en/article/how-to-set-a-custom-domain-for-n8n-on-your-vps-1trx6oe/)

## Step 3: Set Up a Reverse Proxy for HTTPS (Recommended for Security)

n8n doesn't handle HTTPS natively, so use Nginx or Caddy as a reverse proxy. This exposes your domain securely on port 443.

1. Install Nginx: `sudo apt update && sudo apt install nginx` (on Ubuntu/Debian).
2. Create a config file: `sudo nano /etc/nginx/sites-available/n8n`
    
    `textserver {
        listen 80;
        server_name n8n.yourdomain.com;
    
        location / {
            proxy_pass http://localhost:5678/;
            proxy_set_header Connection '';
            proxy_http_version 1.1;
            chunked_transfer_encoding off;
            proxy_buffering off;
            proxy_cache off;
        }
    }`
    
3. Enable: `sudo ln -s /etc/nginx/sites-available/n8n /etc/nginx/sites-enabled/`
4. Test and restart: `sudo nginx -t && sudo systemctl restart nginx`.
5. For HTTPS: Install Certbot (`sudo apt install certbot python3-certbot-nginx`), then run `sudo certbot --nginx -d n8n.yourdomain.com` to auto-configure SSL.[n8n+1](https://community.n8n.io/t/an-easy-step-by-step-guide-on-how-to-self-host-n8n/6505)

Now, access n8n at `https://n8n.yourdomain.com` (update your env vars to HTTPS if needed).

## Step 4: Test and Verify

- Open a browser: Go to `https://n8n.yourdomain.com` (or HTTP if no SSL).
- Check webhooks: Create a test webhook in n8n—it should show your domain.
- For OAuth (e.g., Google): Update allowed domains in Google's console with your new URL.[n8n](https://community.n8n.io/t/find-n8n-domain-instance-for-self-hosted-n8n/57701)
- If issues: Check logs (`docker logs n8n`), ensure firewall allows ports 80/443 (`sudo ufw allow 80` and `sudo ufw allow 443`), and verify DNS.