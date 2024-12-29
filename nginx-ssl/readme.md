Here's what's new in this multi-site setup:

1. Directory structure:

```bash
project/
├── docker-compose.yml
├── nginx/
│   └── conf.d/
│       ├── ssl-params.conf    # Common SSL settings
│       ├── site1.conf        # Site 1 configuration
│       ├── site2.conf        # Site 2 configuration
│       └── site3.conf        # Site 3 configuration
├── certbot/
│   ├── conf/
│   └── www/
└── sites/
    ├── site1/
    ├── site2/
    └── site3/
```

2. To obtain SSL certificates for all domains:

```bash
# Initial setup for site1
docker-compose run --rm certbot certonly --webroot \
  --webroot-path /var/www/certbot \
  -d site1.com -d www.site1.com \
  --email your-email@example.com --agree-tos --no-eff-email

# Repeat for site2
docker-compose run --rm certbot certonly --webroot \
  --webroot-path /var/www/certbot \
  -d site2.com -d www.site2.com \
  --email your-email@example.com --agree-tos --no-eff-email

# Repeat for site3
docker-compose run --rm certbot certonly --webroot \
  --webroot-path /var/www/certbot \
  -d site3.com -d www.site3.com \
  --email your-email@example.com --agree-tos --no-eff-email
```

Key improvements in this setup:

1. **Separate Configuration Files**: Each site has its own configuration file for better organization
2. **Default Server Block**: Added to handle undefined domains securely
3. **WWW Support**: Each site configuration includes both www and non-www versions
4. **Shared SSL Parameters**: Common SSL settings are separated to avoid repetition
5. **Independent Services**: Each site runs as a separate service in Docker Compose
6. **Security**: Added SSL rejection for undefined domains on 443

To add a new site:

1. Add a new service in docker-compose.yml
2. Create a new server block in the Nginx configuration
3. Obtain an SSL certificate for the new domain
4. Restart the services

Would you like me to explain any part in more detail or help you set up specific customizations for your sites?
