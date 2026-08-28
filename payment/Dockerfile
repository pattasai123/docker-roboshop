FROM python:3.9.25-alpine3.21 AS builder
WORKDIR /opt/app
# Build deps for uwsgi & friends
RUN apk add --no-cache \
    build-base \
    linux-headers \
    pcre-dev
# Only requirements first for caching
COPY requirements.txt .
# Install into /install (just like you did)
RUN pip3 install --prefix=/install -r requirements.txt


# ===========================
# Stage 2: Runtime (Alpine)
# ===========================
FROM python:3.9.25-alpine3.21
EXPOSE 8080
WORKDIR /opt/app
# Runtime deps only
RUN apk add --no-cache pcre
# Create non-root user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
# Copy installed packages from builder
COPY --from=builder /install /usr/local
# Copy app files
COPY --chown=roboshop:roboshop payment.ini *.py requirements.txt .
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"

USER roboshop
CMD ["uwsgi", "--ini", "payment.ini"]
# FROM python:3.11-alpine3.23 AS builder

# RUN apk add --no-cache gcc musl-dev

# WORKDIR /opt/app

# COPY requirements.txt .

# RUN pip3 install --no-cache-dir -r requirements.txt

# COPY *.py .
# COPY *.ini .


# FROM python:3.11-alpine3.23

# ENV CART_HOST=cart \
#     CART_PORT=8080 \
#     USER_HOST=user \
#     USER_PORT=8080 \
#     AMQP_HOST=rabbitmq \
#     AMQP_USER=roboshop \
#     AMQP_PASS=roboshop123

# WORKDIR /opt/app

# COPY --from=builder /opt/app/requirements.txt ./

# RUN pip3 install --no-cache-dir -r requirements.txt && \
#     adduser -D roboshop

# COPY --from=builder /opt/app/*.py ./
# COPY --from=builder /opt/app/*.ini ./

# USER roboshop

# CMD ["uwsgi", "--ini", "payment.ini"]