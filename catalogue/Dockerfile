FROM node:20-alpine AS builder
# RUN useradd roboshop
WORKDIR /opt/app
COPY *.js .
COPY *.json .
RUN npm install 

FROM node:20-alpine
WORKDIR /opt/app
COPY --from=builder /opt/app/*.js ./
COPY --from=builder /opt/app/*.js ./
RUN install --omit=dev && \
    useradd -D roboshop
ENV MONGO=true \
MONGO_URL="mongodb://mongodb:27017/catalogue"
USER roboshop
CMD [ "node","server.js" ]