FROM nginx:1.17

#Copying in a new default configuration file along with our Craft project's web folder
COPY ./docker-containers/nginx/default.conf /etc/nginx/conf.d/default.conf
COPY ./docker-containers/nginx/nginx-partials/ /etc/nginx/nginx-partials/
COPY --chown=www-data:www-data ./src/web /var/www/html/web