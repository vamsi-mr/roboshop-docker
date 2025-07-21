# FROM node:20-alpine3.21
# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install
# RUN chown -R roboshop:roboshop /opt/server
# USER roboshop
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD [ "node", "server.js" ]



#Multi Stage Docker Build
### Image Builder
FROM node:20-alpine3.21 AS builder
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install

### Final Image
FROM node:20-alpine3.21
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
WORKDIR /opt/server
USER roboshop
COPY --chown=roboshop:roboshop --from=builder /opt/server /opt/server
CMD [ "node", "server.js" ]
