FROM node:lts as build

RUN apt-get update

RUN apt-get install -y bash mc curl git
RUN apt-get install -y python3

WORKDIR /app
COPY hubs .

RUN npm ci
