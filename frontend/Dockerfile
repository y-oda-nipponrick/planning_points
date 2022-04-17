FROM node:alpine

WORKDIR /myapp

RUN apk update && \
  yarn global add create-nuxt-app

COPY package.json yarn.lock ./

ENV NODE_OPTIONS=--openssl-legacy-provider

RUN yarn -D

CMD [ "yarn" "dev" ]
