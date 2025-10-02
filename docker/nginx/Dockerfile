FROM nginx:1.28.0

# Copy nginx config
COPY ./docker/nginx/default.conf /etc/nginx/conf.d/default.conf

# Create de app directory
RUN mkdir /app

RUN chown -R www-data:www-data /usr/share/nginx/html/
RUN chmod -R 755 /usr/share/nginx/html/