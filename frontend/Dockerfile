FROM nginx:alpine3.24
RUN rm -rf /usr/share/nginx/html/index.html && \
    rm -rf /etc/nginx/nginx.conf
# RUN rm -rf /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf && \
    static /usr/share/nginx/html/