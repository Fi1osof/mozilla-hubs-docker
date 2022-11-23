FROM node:lts-slim

WORKDIR /app
COPY spoke .
RUN apt-get update && apt-get install -y git
RUN apt-get install -y mc

RUN yarn install

CMD scripts/run-local-reticulum.sh
