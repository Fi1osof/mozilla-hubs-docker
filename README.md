# Not production! Just for fun

## Requirements
- docker >= 20.10.14
- docker-compose >= 1.25.0

# Before development

## Add local hosts
```bash
sudo tee -a /etc/hosts > /dev/null <<EOT
127.0.0.1   hubs.local
127.0.0.1   hubs-proxy.local
127.0.0.1   hubs-assets.local
127.0.0.1   hubs-link.local
EOT
```

# Development

## clone repo with submodules
```bash
git clone --recurse-submodules https://github.com/Fi1osof/moz-hubs-docker
cd moz-hubs-docker
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

## Visit https://hubs.local:8080
