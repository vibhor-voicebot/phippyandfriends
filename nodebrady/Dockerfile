# Build
#FROM node:carbon AS base
FROM node:latest AS base

WORKDIR /app

# Dependencies
FROM base AS dependencies  

# A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./
COPY . /app
COPY --from=dependencies /app/package.json ./
COPY --from=dependencies /app ./

# Install app dependencies including 'devDependencies'
RUN apt-get update && apt-get install -y \
    software-properties-common \
    npm
RUN npm install npm@latest -g && \
    npm install n -g && \
    n latest
    
EXPOSE 3000
CMD [ "npm", "start" ]
