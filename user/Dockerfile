FROM node:20
WORKDIR /opt/server
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/users" \
    REDIS_RUL="redis://redis:6379"
COPY package.json .
COPY *.js .
RUN npm install
CMD [ "node", "server.js" ]
