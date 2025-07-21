# -------------------
# Stage 1: Build
# -------------------
FROM python:3.9 AS builder
WORKDIR /opt/server
COPY requirements.txt .
COPY *.py .
COPY package.ini .
RUN pip3 install -r requirements.txt

# --------------------
# Stage 2: Final image
# --------------------
FROM python:3.9.23-alpine3.22
EXPOSE 8080
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
USER roboshop
COPY --chown=roboshop:roboshop --from=builder /opt/server /opt/server/
CMD [ "uwsgi", "--ini", "payment.ini" ]



# FROM python:3.9
# EXPOSE 8080
# WORKDIR /opt/server
# COPY requirements.txt .
# COPY *.py . 
# COPY payment.ini .
# RUN pip3 install -r requirements.txt
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASSWORD="roboshop123"
# CMD [ "uwsgi", "--ini", "payment.ini" ]

