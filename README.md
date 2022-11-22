# Attension! Work in progress. Not for production

## Requirements
- docker 20.10.14
- docker-compose 1.25.0

# Before development

## Add local hosts
```bash
sudo tee -a /etc/hosts > /dev/null <<EOT
127.0.0.1   hubs.local
127.0.0.1   hubs-proxy.local
127.0.0.1   hubs-assets.local
127.0.0.1   hubs-link.local
127.0.0.1   dialog
EOT
```

# Development

## clone repo with submodules
```bash
git clone --recurse-submodules https://github.com/Fi1osof/mozilla-hubs-docker
cd mozilla-hubs-docker
```

## first run db
```bash
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --build db
```

## run reticulum
```bash
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --build reticulum
```

## run other containers
```bash
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --build
```

### Visit https://dialog:4443 and accept self-signet certificate and close this window.

### Visit https://hubs.local:4000 and accept self-signet certificate and close this window.

### Visit https://hubs.local:8080 and accept self-signet certificate.
