FROM node:16 as build

WORKDIR /app

COPY dialog/package.json dialog/package-lock.json ./
RUN npm ci

COPY dialog .
RUN mkdir certs && openssl req -x509 -newkey rsa:2048 -sha256 -days 36500 -nodes -keyout certs/privkey.pem -out certs/fullchain.pem -subj '/CN=dialog'

FROM node:16

ARG PERMS_CERT
ENV perms_key=$PERMS_CERT

WORKDIR /app
COPY --from=build /app /app

COPY scripts/docker/run.sh /run.sh
CMD bash /run.sh
