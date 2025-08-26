# FROM nginx
# EXPOSE 80
# RUN rm -rf /usr/share/nginx/html/index.html
# RUN rm -rf /etc/nginx/nginx.conf
# RUN rm -rf /etc/nginx/conf.d/default.conf
# COPY nginx.conf /etc/nginx/nginx.conf
# COPY static /usr/share/nginx/html/



FROM nginx:1.29.0-alpine
# Remove default config
RUN rm /etc/nginx/nginx.conf /etc/nginx/conf.d/default.conf
# Create directories for nginx runtime (cache, logs, ssl)
RUN mkdir -p /var/cache/nginx/client_temp \
             /var/cache/nginx/proxy_temp \
             /var/cache/nginx/fastcgi_temp \
             /var/cache/nginx/uwsgi_temp \
             /var/cache/nginx/scgi_temp \
    && chown -R nginx:nginx /var/cache/nginx \
    && chown -R nginx:nginx /etc/nginx/ \
    && chmod -R 755 /etc/nginx/ \
    && chown -R nginx:nginx /var/log/nginx
# Prepare SSL folder
RUN mkdir -p /etc/nginx/ssl \
    && chown -R nginx:nginx /etc/nginx/ssl \
    && chmod -R 755 /etc/nginx/ssl
# Fix nginx.pid permissions
RUN touch /var/run/nginx.pid \
    && chown -R nginx:nginx /var/run/nginx.pid /run/nginx.pid
# Copy custom nginx config and static files
COPY nginx.conf /etc/nginx/nginx.conf
COPY static /usr/share/nginx/html/
# Switch to non-root user
USER nginx
# Expose port 80
EXPOSE 80
# Start nginx in foreground
CMD ["nginx", "-g", "daemon off;"]
