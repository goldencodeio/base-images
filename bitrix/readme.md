# [Bitrix Web Server](https://hub.docker.com/r/zolotoykod/bxweb)

These image extends [`zolotoykod/web`](https://hub.docker.com/r/zolotoykod/web) with NGINX settup for 1C-Bitrix and cron daemon

```bash
docker pull zolotoykod/bxweb
```

## Docker Image Layout

```
├── nginx
│   └── vhost.common.d
│       ├── 10-location-root.conf       // Rewrite root location setting for bitrix
│       └── 20-bitrix.conf              // Deny direct access for migrations and modules files
└── www
    └── bitrixsetup.php                 // Bitrix web installer
```

## Image Features

Cron daemon is preinstalled in this image, daemon start added to entrypoint and cron task added to crontab for bitrix agents run.
