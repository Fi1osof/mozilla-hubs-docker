FROM node:lts as build

RUN apt-get update

RUN apt-get install bash mc curl git
RUN apt-get install python3

WORKDIR /app
COPY hubs .

RUN npm ci
