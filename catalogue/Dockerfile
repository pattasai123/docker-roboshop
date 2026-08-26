FROM node:20.0.0
# RUN useradd roboshop
WORKDIR /opt/app
COPY *.js .
COPY *.json .
RUN npm install 
ENV MONGO=true \
MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD [ "node","server.js" ]