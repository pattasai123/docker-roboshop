FROM nginx:alpine3.24

RUN rm -f /usr/share/nginx/html/index.html && \
    rm -f /etc/nginx/nginx.conf

COPY nginx.conf /etc/nginx/nginx.conf
COPY static/ /usr/share/nginx/html/