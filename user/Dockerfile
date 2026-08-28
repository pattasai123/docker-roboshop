FROM node:20 AS builder

WORKDIR /opt/app

COPY *.json ./
RUN npm install

COPY *.js ./

FROM node:20

WORKDIR /opt/app

COPY --from=builder /opt/app/node_modules ./node_modules
COPY --from=builder /opt/app/*.json ./
COPY --from=builder /opt/app/*.js ./

RUN useradd -m roboshop

ENV MONGO=true \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"

USER roboshop

CMD ["node", "server.js"]