FROM nginx:1.23.3-alpine
RUN apk add shadow
RUN groupmod -g 1001 nginx && usermod -u 1001 nginx
RUN mkdir /app && mkdir -p /run/nginx
COPY content /app
RUN chown -R nginx:nginx /app /run/nginx /var/cache/nginx
RUN rm /etc/nginx/nginx.conf /etc/nginx/conf.d/default.conf
COPY conf/nginx.conf /etc/nginx/nginx.conf
USER 1001
EXPOSE 8000
