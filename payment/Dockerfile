FROM python:3.11-slim
RUN useradd roboshop
RUN pip3 install -r requirements.txt
WORKDIR /opt/app
COPY *.py .
COPY *.ini .
COPY *.txt .
ENV CART_HOST="cart" \
CART_PORT="8080" \
USER_HOST="user" \
USER_PORT="8080" \
AMQP_HOST="rabbitmq" \
AMQP_USER="roboshop" \
AMQP_PASS="roboshop123"

CMD [ "uwsgi", "--ini", "payment.ini" ]