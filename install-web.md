---
title: Installing and Configuring a Web Node
description: 
published: true
date: 2025-12-09T02:56:55.302Z
tags: 
editor: markdown
dateCreated: 2025-12-09T02:56:55.302Z
---

# Saito Web Node — Manual Installation Guide (Ubuntu 24.04)

This guide explains how to install a Saito Web Node on a fresh Ubuntu 24.04 server.  
It mirrors the behaviour of the automated install script, but allows you to execute each step manually.

---

## 1. Prerequisites & considerations

Before starting:

- Use a fresh Ubuntu **24.04 LTS** installation.  
- Ensure you have **root** or **sudo** access.  
- Choose a domain name (e.g., `node.example.com`).  
- Point the domain’s **A record** at your server’s public IP.  
- Make sure ports **80** and **443** are open.  
- Existing Saito or nginx installations may be overwritten.

---

## 2. Domain setup and DNS verification

Your domain must resolve to your server before SSL certificates can be issued.

Create an **A record**:

```
your.domain.com → YOUR.SERVER.IP
```

Verify DNS:

```bash
dig +short your.domain.com
```

You should see your server’s IP address.

---

## 3. System update and install dependencies

Update the system and install basic build tools:

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y git g++ make python3 python3-pip
```

---

## 4. Install Node.js, npm, TypeScript, and PM2

Saito runs on Node.js. PM2 is used to keep the node running in production.

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
sudo npm install -g typescript
sudo npm install -g pm2
```

---

## 5. Install nginx and Certbot

nginx serves as the reverse proxy. Certbot enables HTTPS via Let’s Encrypt.

```bash
sudo apt install -y nginx certbot python3-certbot-nginx
```

---

## 6. Download Saito and install Node dependencies

Clone the Saito repository into `/opt` and install dependencies.

```bash
cd /opt
sudo git clone https://github.com/saitotech/saito
cd saito/node
sudo npm install
```

If the folder already exists:

```bash
cd /opt/saito
sudo git pull
```

---

## 7. Run Saito initialization

Initialize/reset the Saito node environment.

```bash
cd /opt/saito/node
sudo npm run nuke
```

---

## 8. Configure nginx reverse proxy

Create a new nginx site for your domain. Replace `your.domain.com` with your own:

```bash
sudo tee /etc/nginx/sites-available/your.domain.com > /dev/null << 'EOF'
server {
    listen 80;
    server_name your.domain.com www.your.domain.com;

    gzip on;
    gzip_proxied any;
    gzip_min_length 256;
    gzip_comp_level 9;
    gzip_types text/plain text/css text/xml text/javascript application/javascript application/json application/xml+rss;

    proxy_connect_timeout 300s;
    proxy_send_timeout 300s;
    proxy_read_timeout 300s;

    location ~* \.(css|js|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
        expires 7d;
        add_header Cache-Control "public, immutable";

        proxy_pass http://localhost:12101;
        proxy_set_header Upgrade \$http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host \$host;
        proxy_set_header X-Real-IP \$remote_addr;
        proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto \$scheme;
    }

    location / {
        proxy_pass http://localhost:12101;

        proxy_set_header Upgrade \$http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host \$host;
        proxy_set_header X-Real-IP \$remote_addr;
        proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto \$scheme;

        proxy_http_version 1.1;
        proxy_buffering off;
        proxy_request_buffering off;
    }
}
EOF
```

---

## 9. Enable nginx site and start nginx

Enable the new site and remove the default configuration:

```bash
sudo ln -sf /etc/nginx/sites-available/your.domain.com /etc/nginx/sites-enabled/your.domain.com
sudo rm -f /etc/nginx/sites-enabled/default
```

Test and start nginx:

```bash
sudo nginx -t
sudo systemctl start nginx
sudo systemctl enable nginx
```

---

## 10. Obtain SSL certificate

Enable HTTPS using Certbot:

```bash
sudo certbot --nginx -d your.domain.com -d www.your.domain.com --non-interactive --agree-tos --email admin@your.domain.com
```

If DNS is correct, Certbot updates your nginx config automatically.

---

## 11. Restart nginx

Apply all changes:

```bash
sudo systemctl restart nginx
```

---

## 12. Configure PM2 for Saito

PM2 ensures Saito runs continuously and starts on boot.

Create the PM2 ecosystem config:

```bash
cd /opt/saito/node
sudo tee ecosystem.config.js > /dev/null << 'EOF'
module.exports = {
  apps: [{
    name: 'saito-node',
    script: 'npm start',
    instances: 1,
    exec_mode: 'fork',
    watch: false,
    max_memory_restart: '2G',
    error_file: './logs/err.log',
    out_file: './logs/out.log',
    log_file: './logs/saito.log',
    time: true
  }]
};
EOF
```

Create log directory:

```bash
sudo mkdir -p /opt/saito/node/logs
```

Start and register the PM2 service:

```bash
sudo pm2 start ecosystem.config.js
sudo pm2 save
sudo pm2 startup systemd -u root --hp /root
```

---

## 13. Final checks

Visit your node:

```
https://your.domain.com/
```

Check PM2:

```bash
pm2 status
pm2 logs saito-node
```

If using UFW, allow necessary ports:

```bash
sudo ufw allow 'Nginx Full'
```

Your Saito Web Node should now be running securely over HTTPS and managed by PM2.


