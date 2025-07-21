# -------------------
# Stage 1: Build
# -------------------
FROM maven AS builder
WORKDIR /opt/server
COPY pom.xml .
COPY src /opt/server/src
COPY pom.xml /opt/server/
RUN mvn clean package 


# --------------------
# Stage 2: Final image
# --------------------
FROM eclipse-temurin:17-jre-alpine
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
USER roboshop
COPY --chown=roboshop:roboshop --from=builder /opt/server/target/shipping-*.jar /opt/server/shipping.jar
CMD [ "java", "-jar", "shipping.jar" ]



# FROM maven
# WORKDIR /opt/server
# COPY src /opt/server/src
# COPY pom.xml /opt/server/
# RUN mvn clean package
# RUN mv /opt/server/target/shipping-1.0.jar /opt/server/shipping.jar
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD [ "java", "-jar", "shipping.jar" ]


