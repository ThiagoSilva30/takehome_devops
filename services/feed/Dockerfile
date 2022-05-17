FROM node:latest AS build

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY package*.json /usr/src/app
RUN npm install
COPY . /usr/src/app/

FROM alpine:latest

RUN mkdir -p /app
WORKDIR /app
COPY --from=build /usr/src/app/ /app 
RUN apk add openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community
RUN apk update && apk add nodejs && apk add npm
RUN npm run release

#EXPOSE 3000
ENTRYPOINT USERINFO_URL=http://localhost:8037/api/userinfo npm run start
