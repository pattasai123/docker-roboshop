FROM maven:latest
RUN useradd roboshop
WORKDIR /opt/app
COPY src/ .
COPY *.xml .
RUN mvn clean package
RUN mv target/shipping-1.0.jar shipping.jar
ENV CART_ENDPOINT="cart:8080" \
DB_HOST="mysql"
CMD [ "java", "-jar","shipping.jar" ]
RUN dnf install mysql -y 
