FROM maven:3.9-eclipse-temurin-17 AS builder

WORKDIR /opt/app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests && \
    mv target/shipping-1.0.jar shipping.jar


FROM eclipse-temurin:17-jre-alpine
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/app
ENV CART_ENDPOINT=cart:8080 \
    DB_HOST=mysql
COPY --from=builder --chown=roboshop:roboshop /opt/app/shipping.jar shipping.jar
USER roboshop
CMD ["java", "-jar", "shipping.jar"]