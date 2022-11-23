# Attension! Work in progress. Not for production

## Requirements specified versions
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

## Mail server
For local debug only
```bash
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --build mail
```
Visit http://localhost:8025


## DB
```bash
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --build db
```

## Reticulum

### Edit reticulum/reticulum/config/dev.exs
Replace 
```yml 
config :ret, Ret.Mailer, adapter: Bamboo.LocalAdapter
```

with
```yml 
config :ret, Ret.Mailer, adapter: Bamboo.LocalAdapter,
  # add
  server: "mail",
  port: 1025,
  tls: :never,
  tls_verify: :verify_none,
  # other config editable
  hostname: "hubs.local",
  username: "hubs@hubs.local",
  retries: 3
```

### run reticulum server
```bash
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --build reticulum
```
Visit https://hubs.local:4000 and accept self-signet certificate and close this window.


## Dialog
```bash
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --build dialog
```
Visit https://dialog:4443 and accept self-signet certificate and close this window.


## Hubs
```bash
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --build hubs
```

Visit https://hubs.local:8080 and accept self-signet certificate.


## Spoke

```bash
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --build spoke
```
Vitis https://hubs.local:9090 and accept self-signet certificate.
