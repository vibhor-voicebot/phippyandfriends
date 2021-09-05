ARG NODE_VERSION=11

###
# 1. Dependencies
###

FROM node:${NODE_VERSION}-slim as dependencies
WORKDIR /app

RUN apt-get update && apt-get install -y software-properties-common npm
RUN npm install --global npm node-gyp

COPY package.json *package-lock.json *.npmrc ./

ARG NODE_ENV=production
ENV NODE_ENV ${NODE_ENV}
RUN npm ci

###
# 2. Application
###

FROM node:${NODE_VERSION}-slim
WORKDIR /app

COPY --from=dependencies /app/node_modules node_modules
COPY . .

ENV PATH="$PATH:/app/node_modules/.bin"
ENV PORT 3000

EXPOSE 3000

CMD ["node", "app.js"]
