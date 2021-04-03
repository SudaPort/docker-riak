FROM nginx:stable-alpine-perl

COPY ./hosts /etc/nginx/conf.d
COPY entrypoint.sh /
COPY ./ssl-cert /etc/nginx/ssl

ENTRYPOINT ["chmod", "+x", "/entrypoint.sh"]