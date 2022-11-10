FROM node:lts as build

WORKDIR /app
COPY dialog .
RUN mkdir certs && openssl req -x509 -newkey rsa:2048 -sha256 -days 36500 -nodes -keyout certs/privkey.pem -out certs/fullchain.pem -subj '/CN=dialog'
RUN npm ci


FROM node:lts-slim

ARG PERMS_CERT
ENV perms_key=$PERMS_CERT

WORKDIR /app
COPY --from=build /app /app
# RUN apt-get update && apt-get install -y jq curl dnsutils netcat
# RUN apt-get install -y mc

# COPY dialog/scripts/docker/run.sh /run.sh
COPY scripts/docker/run.sh /run.sh
CMD bash /run.sh
