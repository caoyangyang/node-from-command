FROM node:carbon-alpine

# Create app directory
RUN mkdir -p /app
WORKDIR /app

# Bundle app source
COPY server /app/server
COPY *.json /app/
RUN  npm install pm2 -g

EXPOSE 4455
CMD [ "pm2", "start","server/index.js" ]
