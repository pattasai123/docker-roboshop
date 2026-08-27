FROM node:20-alpine AS builder
# RUN useradd roboshop
WORKDIR /opt/app
COPY *.js .
COPY *.json .
RUN npm install 

FROM node:20-alpine
WORKDIR /opt/app
COPY --from=builder /opt/app/*.js ./
COPY --from=builder /opt/app/*.json ./
RUN npm install --omit=dev && \
    useradd -D roboshop 
ENV MONGO=true \
REDIS_URL="redis://redis:6379" \
MONGO_URL="mongodb://mongodb:27017/users"
USER roboshop
CMD [ "node","server.js" ]