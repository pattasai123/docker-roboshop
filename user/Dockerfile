FROM node:20.0.0
# RUN useradd roboshop
WORKDIR /opt/app
COPY *.js .
COPY *.json .
RUN npm install 
ENV MONGO=true \
REDIS_URL="redis://redis:6379" \
MONGO_URL="mongodb://mongodb:27017/users"
CMD [ "node","server.js" ]