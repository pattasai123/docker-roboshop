FROM python:3.11-alpine3.23 AS builder

RUN apk add --no-cache gcc musl-dev

WORKDIR /opt/app

COPY requirements.txt .

RUN pip3 install --no-cache-dir -r requirements.txt

COPY *.py .
COPY *.ini .


FROM python:3.11-alpine3.23

ENV CART_HOST=cart \
    CART_PORT=8080 \
    USER_HOST=user \
    USER_PORT=8080 \
    AMQP_HOST=rabbitmq \
    AMQP_USER=roboshop \
    AMQP_PASS=roboshop123

WORKDIR /opt/app

COPY --from=builder /opt/app/requirements.txt ./

RUN pip3 install --no-cache-dir -r requirements.txt && \
    adduser -D roboshop

COPY --from=builder /opt/app/*.py ./
COPY --from=builder /opt/app/*.ini ./

USER roboshop

CMD ["uwsgi", "--ini", "payment.ini"]