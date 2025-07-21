# FROM maven
# WORKDIR /opt/server
# COPY src /opt/server/src
# COPY pom.xml /opt/server/
# RUN mvn clean package
# RUN mv /opt/server/target/shipping-1.0.jar /opt/server/shipping.jar
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD [ "java", "-jar", "shipping.jar" ]



### Multi Stage Docker Build
### Image Builder
FROM maven AS bullder
WORKDIR /opt/server
COPY pom.xml .
COPY src /opt/server/src
COPY pom.xml /opt/server/
RUN mvn clean package 

## Final Image
FROM eclipse-temurin:17-jre-alpine
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
COPY --chown=roboshop:roboshop --from=builder /opt/server/target/shipping-*.jar /opt/server/shipping.jar
CMD [ "java", "-jar", "shipping.jar" ]

