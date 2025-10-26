# Docker Nginx Certbot

A Docker Compose setup that provides Nginx with automatic SSL certificate management using Let's Encrypt via Certbot.

## Overview

This project sets up:
- **Nginx** web server (1.29-alpine) running in host network mode
- **Certbot** for automatic SSL certificate generation and renewal
- Persistent volumes for certificates, configuration, and web content

## Services

### Web (Nginx)
- Image: `nginx:1.29-alpine`
- Network mode: `host` (shares host network stack)
- Environment variables:
  - `LETSENCRYPT_HOST`: Domain name for SSL certificate
  - `LETSENCRYPT_EMAIL`: Email for Let's Encrypt notifications
- Volumes:
  - `html`: Web content directory
  - `certbot`: Read-only access to Certbot challenge files
  - `certs`: Read-only access to SSL certificates
  - `conf`: Nginx configuration files

### Certbot
- Image: `certbot/certbot:v4.2.0`
- Volumes:
  - `certbot`: Challenge files for domain validation
  - `certs`: Generated SSL certificates

## Usage

1. Create a `.env` file with your domain and email:
   ```env
   LETSENCRYPT_HOST=yourdomain.com
   LETSENCRYPT_EMAIL=your@email.com
   ```

2. Start the services:
   ```bash
   docker-compose up -d
   ```

3. Place your web content in the `html` volume or mount your content directory.

## Volumes

- `html`: Web content served by Nginx
- `certbot`: Let's Encrypt challenge files
- `certs`: SSL certificates and keys
- `conf`: Nginx configuration files

## Configuration

The project includes:
- `.gitignore`: Excludes local override files
- `renovate.json`: Automated dependency updates configuration

## Notes

- The Nginx container runs in host network mode, which means it directly uses the host's network interfaces.
- SSL certificates are automatically managed by Certbot and stored in persistent volumes.
- The setup is designed for production use with automatic restart policies.