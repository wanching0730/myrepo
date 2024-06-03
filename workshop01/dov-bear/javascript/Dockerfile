FROM node:22-bullseye

## Build the application

# create and CD into directory
WORKDIR /app

# Inside /app directory

# Copy all sources into the image
COPY package.json .
COPY package-lock.json .
COPY main.js .
COPY public public
COPY views views

# Install the dependencies
RUN npm ci


## Run the application

# Environment variable used by the application
ENV PORT=5000
ENV INSTANCE_NAME=hello
ENV INSTANCE_HASH=cayenne

# Ports that the application bind to
EXPOSE ${APP_PORT}

# Run
ENTRYPOINT node main.js