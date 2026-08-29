FROM node:20.19.5-alpine3.21 AS builder
WORKDIR /opt/app
COPY *.json ./
COPY *.js ./
RUN npm install

FROM node:20.19.5-alpine3.21

WORKDIR /opt/app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
COPY --from=builder --chown=roboshop:roboshop /opt/app /opt/app

ENV MONGO=true \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"

USER roboshop

CMD ["node", "server.js"]
# FROM node:20 AS builder
# WORKDIR /opt/app
# COPY *.json ./
# COPY *.js ./
# RUN npm install

# FROM node:20

# WORKDIR /opt/app
# # COPY --from=builder /opt/app/node_modules ./node_modules
# # COPY --from=builder /opt/app/*.json ./
# # COPY --from=builder /opt/app/*.js ./

# # RUN useradd -m roboshop

# ENV MONGO=true \
#     REDIS_URL="redis://redis:6379" \
#     MONGO_URL="mongodb://mongodb:27017/users"

# USER roboshop

# CMD ["node", "server.js"]