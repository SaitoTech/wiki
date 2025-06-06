---
title: Deploy Saito Instance
description: 
published: true
date: 2025-05-19T17:12:08.721Z
tags: installation
editor: markdown
dateCreated: 2023-02-23T07:15:16.260Z
---

# Deploy Saito on a VPS or server - Ubuntu 22.04 (LTS) x64

This page provides a quick guide to deploying Saito on a VPS or server. It will walk you through the process of handling the common supplemental problems like getting an SSL cert and customizing your configuration files so you can access your Saito install remotely instead of through localhost.

Before you start, be sure you've completed the [installation instructions](/install) for the standard Saito client and have successfully installed [Saito](https://github.com/saitotech/saito) on your own machine before continuing. The rest of this write-up assumes basic familiarity with the process of doing so.

<hr>

## Configuration

Generate a custom options file that includes the host and port that you will expose publicly on your server -- make an `options.conf` in the `config/` folder with the following content; be sure to set your endpoint to your domain:
```
{
	"server":{
		"host":"localhost",
		"port":12101,
		"protocol":"http"
		"endpoint":{
			"host":"your_domain.com",
			"port":12101,
			"protocol":"http"
		}
	}
}
```

## WebServer, reverse proxy and HTTPS
Make sure to point your domain to the same VPS or server that will run Saito.

The following instructions assume you are using ***NGINX*** as your webserver and secure it with Let's Encrypt. Alternatives webservers should follow the same logic, please refer to your service's manual/documentation.

```
sudo apt-get update
sudo apt-get install nginx
```
#### 1) Configure NGINX as a reverse proxy

Add the server block config on `/etc/nginx/sites-enable/<file_name>`
Your saito installation will point to localhost:12101 by default
```
server {
    server_name yourdomain.com;
    location / {
        proxy_pass http://localhost:12101;
    }
}
```
Now you can visit Saito in your browser visiting `http://yourdomain.com`

#### 2) Secure NGINX with Let's Encrypt (HTTPS)
```
sudo apt-get install certbot python3-certbot-nginx
```
Obtain an SSL Certificate with:
```
sudo certbot --nginx -d yourdomain.com
```
...and follow the prompts. 
To check config is correct and restart NGINX run:
```
nginx -t
systemctl restart nginx
```

Now that you have a secure connection to your node we need to change the endpoint from your config file (`config/options.conf`) to the default secure port and protocol:
```
{
	"server":{
		"host":"localhost",
		"port":12101,
		"protocol":"http"
		"endpoint":{
			"host":"yourdomain.com",
			"port":443,
			"protocol":"https"
		}
	}
}
```
Compile your Saito (`npm run nuke`) and if everything is correct you can visit your Saito with `https://yourdomain.com`

#### 3) Enable websockets for NGINX
Add the following config on your server block `/etc/nginx/sites-enable/<file_name>` config file with:
```
server {
    server_name yourdomain.com;
    location / {
        proxy_pass http://localhost:12101;
        
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_http_version 1.1;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
    }
}
```

#### 4) Enable Cross-origin Resource sharing (CORS) for NGINX

Add the following config on your server block `/etc/nginx/sites-enable/<file_name>` config file with:
```
#
# Wide-open CORS config for nginx
#
location / {
     if ($request_method = 'OPTIONS') {
        add_header 'Access-Control-Allow-Origin' '*';
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
        #
        # Custom headers and headers various browsers *should* be OK with but aren't
        #
        add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range';
        #
        # Tell client that this pre-flight info is valid for 20 days
        #
        add_header 'Access-Control-Max-Age' 1728000;
        add_header 'Content-Type' 'text/plain; charset=utf-8';
        add_header 'Content-Length' 0;
        return 204;
     }
     if ($request_method = 'POST') {
        add_header 'Access-Control-Allow-Origin' '*' always;
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS' always;
        add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range' always;
        add_header 'Access-Control-Expose-Headers' 'Content-Length,Content-Range' always;
     }
     if ($request_method = 'GET') {
        add_header 'Access-Control-Allow-Origin' '*' always;
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS' always;
        add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range' always;
        add_header 'Access-Control-Expose-Headers' 'Content-Length,Content-Range' always;
     }
}
```
#### 5) Enable compression for NGINX
Add the following config on your server block `/etc/nginx/sites-enable/<file_name>` config file with:
```
server {
    ...
    
    gzip on;
    gzip_vary on;
    gzip_proxied any;
    gzip_comp_level 9;
    gzip_http_version 1.1;
    gzip_min_length 1024;
    gzip_types application/atom+xml application/geo+json application/javascript application/x-javascript application/json application/ld+json application/manifest+json application/rdf+xml application/rss+xml application/xhtml+xml application/xml font/eot font/otf font/ttf image/svg+xml text/css text/javascript text/plain text/xml;
    
    ...
    location / {
        ...
    }
}

```

Check config is correct and restart NGINX
```
nginx -t
systemctl restart nginx
```
And done!













<!--

Requirements:
- Machine with at least 2GB RAM.
- Domain
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript
---
## 1) Install Dependencies
SSH to your VPS and run:
```
sudo apt-get update
sudo apt-get install g++ make git python3
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash
sudo apt-get install -y nodejs
```

## 2) Download Saito
```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
npm install
```
> note: in case npm fails to install a module, you might need to `sudo apt-get install python-is-python3`.
## 3) Compile and Run Saito
```
npm run nuke
npm start
```
## 4) Visit Saito in your Browser
Once you have run ```npm start``` it will take a few moments for the Saito software to initialize and start. You will eventually see an animated Saito logo scroll across your terminal. Once that is done simply open a browser and visit:
> http://localhost:12101


To visit your Saito instance on your VPS:
>http://<your_server_ip>:12101

To generate a custom options file make a `options.conf` on `config/` folder, now set your endpoint to your domain with the following:
```
{
	"server":{
		"host":"localhost",
		"port":12101,
		"protocol":"http"
		"endpoint":{
			"host":"your_domain.com",
			"port":12101,
			"protocol":"http"
		}
	}
}
```
Compile with ```npm run nuke```, final compiled file is on config/options
-->