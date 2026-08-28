FROM node:20-alpine AS builder

WORKDIR /opt/app

COPY *.json ./
RUN npm install

COPY *.js ./

FROM node:20-alpine

WORKDIR /opt/app

COPY --from=builder /opt/app/node_modules ./node_modules
COPY --from=builder /opt/app/*.json ./
COPY --from=builder /opt/app/*.js ./

RUN adduser -D roboshop

ENV REDIS_HOST="redis" \
    CATALOGUE_HOST="catalogue" \
    CATALOGUE_PORT="8080"

USER roboshop

CMD ["node", "server.js"]

# FROM node:20-alpine AS builder
# # RUN useradd roboshop
# WORKDIR /opt/app
# COPY *.js .
# COPY *.json .
# RUN npm install 

# FROM node:20-alpine
# WORKDIR /opt/app
# COPY --from=builder /opt/app/*.js ./
# COPY --from=builder /opt/app/*.json ./
# RUN npm install --omit=dev && \
#     useradd -D roboshop
# ENV REDIS_HOST="redis" \
# CATALOGUE_HOST="catalogue" \
# CATALOGUE_PORT="8080"
# USER roboshop
# CMD [ "node","server.js" ]

# FROM node:20.0.0
# # RUN useradd roboshop
# WORKDIR /opt/app
# COPY *.js .
# COPY *.json .
# RUN npm install 
# ENV REDIS_HOST="redis" \
# CATALOGUE_HOST="catalogue" \
# CATALOGUE_PORT="8080"
# CMD [ "node","server.js" ]