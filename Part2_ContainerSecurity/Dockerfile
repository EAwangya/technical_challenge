FROM nginx:1.27-alpine
WORKDIR /usr/share/nginx/html
COPY index.html .
COPY nginx.conf /etc/nginx/conf.d/default.conf
RUN addgroup -S web \
    && adduser -S web -G web \
    && chown -R web:web /var/cache/nginx /var/run /var/log/nginx \
    && chown -R web:web /usr/share/nginx/html
USER web
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]