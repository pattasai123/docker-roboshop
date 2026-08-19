FROM python:3.11-slim

RUN apt-get update && apt-get install -y gcc

RUN useradd roboshop

WORKDIR /opt/app

COPY requirements.txt .

RUN pip3 install -r requirements.txt

COPY *.py .
COPY *.ini .

ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"

CMD ["uwsgi", "--ini", "payment.ini"]