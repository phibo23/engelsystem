FROM nginx:alpine as es_nginx
RUN mkdir -p /var/www/public/ && touch /var/www/public/index.php
COPY docker/nginx/nginx.conf /etc/nginx/nginx.conf

FROM node:10-alpine as themes
WORKDIR /app
COPY .babelrc .browserslistrc package.json webpack.config.js yarn.lock /app/
RUN yarn install
COPY resources/assets/ /app/resources/assets
RUN yarn build

FROM es_nginx
COPY --from=themes /app/public/assets /var/www/public/assets/
