# -------------------
# Stage 1: Build
# -------------------
FROM node:20-alpine3.21 AS builder
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install


# --------------------
# Stage 2: Final image
# --------------------
FROM node:20-alpine3.21
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop 
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/users" \
    REDIS_URL="redis://redis:6379"
WORKDIR /opt/server
USER roboshop
COPY --chown=roboshop:roboshop --from=builder /opt/server /opt/server
CMD [ "node", "server.js" ]




# FROM node:20
# WORKDIR /opt/server
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/users" \
#     REDIS_RUL="redis://redis:6379"
# COPY package.json .
# COPY *.js .
# RUN npm install
# CMD [ "node", "server.js" ]

