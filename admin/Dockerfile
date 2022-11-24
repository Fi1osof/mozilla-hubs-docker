FROM node:lts-slim

RUN apt-get update

RUN apt-get install -y bash mc curl git
RUN apt-get install -y python3

WORKDIR /app

COPY admin .
RUN npm ci

WORKDIR /app/admin

# admin/admin folder uses node_modules from parent folder
RUN npm ci
