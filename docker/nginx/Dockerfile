FROM nginx:1.17.7

RUN apt update
RUN apt install -y less nano

COPY default.conf /etc/nginx/conf.d/
#COPY fastcgi-php.conf /etc/nginx/
#COPY fastcgi.conf /etc/nginx/