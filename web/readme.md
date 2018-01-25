# [Web](https://hub.docker.com/r/zolotoykod/web)

Base NGINX + PHP-FPM Web Server

```bash
docker pull zolotoykod/web
```

## Docker Image Layout

```
├── nginx                               // NGINX configuration /etc/nginx
│   ├── conf.d
│   │   └── upstream.conf               // Init PHP upstream
│   ├── nginx.conf                      // Base NGINX server config
│   ├── sites-available
│   │   └── default                     // Default host config, includes vhost.common.d/*.conf;
│   └── vhost.common.d                  // Vhost configuration directory
│       ├── 10-general.conf             // General vhost settings (client_max_body_size etc)
│       ├── 10-location-root.conf       // Redirect requests to DOCUMENT_INDEX
│       ├── 10-php.conf                 // PHP cgi configuration for vhost
│       └── 20-common-routes.conf       // Turn off log for robots.txt and favicon.ico
│                                       // Enable caching for assets
│                                       // Deny direct access for .git, vendor and composer files
├── php
│   ├── 30-php.ini                      // Base PHP settings
│   ├── 30-ssmtp.ini.disabled           // Use ssmtp for mail function
│   └── 30-xdebug.ini.disabled          // Enable Xdebug
└── sbin
    └── entrypoint                      // Start nginx service and php-fpm
```

## Quick tips

### Enable SMTP support

This image has ssmtp package preinstalled. So you can add this lines to your Dockerfile to enable smtp support:

```dockerfile
# enable ssmtp
RUN mv /etc/php/7.1/fpm/conf.d/30-mail.ini.disabled /etc/php/7.1/fpm/conf.d/30-mail.ini &&
	mv /etc/php/7.1/cli/conf.d/30-mail.ini.disabled /etc/php/7.1/cli/conf.d/30-mail.ini

# ssmtp config
RUN { \
	echo "mailhub=mail.zolotoykod.ru"; \
	echo "FromLineOverride=YES"; \
} >> /etc/ssmtp/ssmtp.conf

# default sender email
RUN { \
	echo "root:noreply@zolotoykod.ru:mail.zolotoykod.ru"; \
	echo "www-data:noreply@zolotoykod.ru:mail.zolotoykod.ru"; \
} >> /etc/ssmtp/revaliases
```

### Enable Xdebug

1. On your development environment attach to container

    ```bash
    docker-compose exec <service_name> bash
    // or
    docker exec -it <container_id> bash
    ```

1. Enable Xdebug config

    ```bash
    cd /etc/php/7.1/fpm/conf.d/
    mv 30-xdebug.ini.disabled 30-xdebug.ini
    ```

1. Rewrite Xdebug settings [Optional]

    You also can set your custom settings for Xdebug. To do this add `95-custom-xdebug.ini` in `/etc/php/7.1/fpm/conf.d/`

1. Restart container

    ```bash
    docker-compose restart <service_name>
    // or
    docker restart <container_id>
    ```
