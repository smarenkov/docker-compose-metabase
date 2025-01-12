# Docker Compose Metabase

> Self-hosted Metabase setup using Docker Compose.

## Overview

This repository contains a Docker Compose setup for running a self-hosted Metabase instance with PostgreSQL as the persistence database.

## Getting started

Follow these steps to set up, configure, and deploy project.

### Environment Setup

1. Duplicate the `.env.example` file:
```bash
cp .env.example .env
```

2. Fill out all required environment variables in the `.env` file.

### Configure Nginx

1. Create an Nginx configuration file for your domain at `/etc/nginx/sites-enabled/{your_domain}`:
```conf
server {
    listen 80;
    server_name your_domain #example metabase.smarenkov.dev;

    location / {
            proxy_pass http://127.0.0.1:3000;
    }
}
```

2. Create a symbolic link to enable the site:
```bash
ln -s /etc/nginx/sites-enabled/{your_domain} /etc/nginx/sites-available/{your_domain}
```

### Deployment

1. Transfer the `.env` and `docker-compose.yaml` files to your server:
```bash
scp .env docker-compose.yaml your_user@your_server:/docker-compose-metabase/
```
1. Start Docker containers
```bash
ssh your_user@your_server "cd /docker-compose-metabase/ && docker-compose up --build -d"
```

## Additional Notes
• For HTTPS support, set up SSL/TLS certificates using a tool like [Certbot](https://certbot.eff.org/).