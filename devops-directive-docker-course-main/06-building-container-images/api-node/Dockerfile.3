# Pin specific version for stability
# Use slim for reduced image size
FROM node:19.6-bullseye-slim

# Specify working directory other than /
WORKDIR /usr/src/app

# Copy only files required to install dependencies (better layer caching)
# this will copy package.json and package-lock.json files
COPY package*.json ./

RUN npm install

# Copy remaining source code AFTER installing dependencies.
# Again, copy only the necessary files
COPY ./src/ .

CMD [ "node", "index.js" ]
