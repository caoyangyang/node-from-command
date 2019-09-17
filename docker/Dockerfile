FROM node:carbon-alpine

# Create app directory
RUN mkdir -p /app
WORKDIR /app

# Bundle app source
COPY server /app/server
COPY *.json /app/

EXPOSE 4455
CMD [ "node", "server/index.js" ]
