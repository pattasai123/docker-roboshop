FROM maven:3.9-eclipse-temurin-17 AS builder

WORKDIR /opt/app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests && \
    mv target/shipping-1.0.jar shipping.jar


FROM eclipse-temurin:17-jre-alpine

WORKDIR /opt/app

COPY --from=builder /opt/app/shipping.jar shipping.jar
RUN useradd -D roboshop
ENV CART_ENDPOINT=cart:8080 \
    DB_HOST=mysql
USER roboshop
CMD ["java", "-jar", "shipping.jar"]