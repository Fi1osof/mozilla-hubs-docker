FROM node:16

WORKDIR /app
COPY spoke .

# git submodule make errors
RUN rm .git -rf

RUN apt-get update && apt-get install -y git

RUN yarn install
