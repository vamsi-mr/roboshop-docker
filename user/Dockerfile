# FROM node:20
# WORKDIR /opt/server
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/users" \
#     REDIS_RUL="redis://redis:6379"
# COPY package.json .
# COPY *.js .
# RUN npm install
# CMD [ "node", "server.js" ]


### Multi Stage Docker Build
### Image Builder
FROM node:20-alpine3.21 AS builder
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install

### Final Image
FROM node:20-alpine3.21
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop 
RUN chown -R roboshop:roboshop /opt/server
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/users" \
    REDIS_RUL="redis://redis:6379"
USER roboshop
COPY --from=builder /opt/server /opt/server
CMD [ "node", "server.js" ]




