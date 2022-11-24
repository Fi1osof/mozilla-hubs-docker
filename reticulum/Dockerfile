
# certs
FROM alpine/openssl as certr
WORKDIR /certs
RUN openssl req -x509 -newkey rsa:2048 -sha256 -days 36500 -nodes -keyout key.pem -out cert.pem -subj '/CN=ret' && cp cert.pem cacert.pem


# reticulum
FROM elixir:1.9-alpine

ARG PERMS_KEY
ENV PERMS_KEY=$PERMS_KEY

ENV POSTGREST_INTERNAL_HOSTNAME=db
ENV DB_HOST=db
ENV DIALOG_HOSTNAME=localhost
ENV DIALOG_PORT=4443

# https://hex.pm/docs/mirrors
ENV HEX_MIRROR=https://cdn.jsdelivr.net/hex

RUN apk update
RUN apk add --no-cache bash openssl-dev openssl jq libstdc++ coreutils curl mc git
RUN apk add --no-cache ansible inotify-tools

WORKDIR /ret

COPY --from=certr /certs .

COPY reticulum .

# For postgREST
# https://github.com/mozilla/hubs-ops/wiki/Running-PostgREST-locally
COPY reticulum-jwk.json .

RUN mkdir -p storage/dev

RUN mix local.hex --force
RUN mix local.rebar --force
RUN mix deps.get
RUN mix ecto.create
