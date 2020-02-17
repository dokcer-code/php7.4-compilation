FROM ubuntu:18.04
RUN apt update
RUN apt install -y wget gcc htop nano less
RUN apt install -y pkg-config libxml2-dev libsqlite3-dev libonig-dev
# RUN apt install -y libxml2-dev libjpeg-dev libpng-dev libfreetype6-dev libbz2-dev libmcrypt-dev libxslt1-dev
RUN wget https://www.php.net/distributions/php-7.4.2.tar.gz  --output-document=/usr/local/src/php-7.4.2.tar.gz
RUN tar -C "/usr/local/src" -xzvf /usr/local/src/php-7.4.2.tar.gz
WORKDIR "/usr/local/src/php-7.4.2"
RUN ./configure --build=x86_64-linux-gnu --prefix=/opt/php-7.4.2 --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data --with-config-file-path=/opt/etc/php \
    --with-config-file-scan-dir=/opt/etc/php/conf.d --with-pdo-mysql --with-mhash --enable-ftp --with-libdir=lib/x86_64-linux-gnu --enable-mbstring
#RUN ./configure --prefix=/opt/php-5.4.45 --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data --with-pdo-mysql --enable-mbstring --enable-sockets \
#    --enable-exif --enable-bcmath --enable-calendar --enable-zip --enable-ftp --enable-gd-native-ttf --with-gd --with-freetype-dir -with-zlib --with-bz2 \
#    --with-mcrypt -with-mhash --with-pcre-regex --with-xmlrpc --with-xsl -with-mysql --enable-intl --with-gettext
RUN make
RUN make install
COPY php-fpm.conf /opt/php-7.4.2/etc/
COPY www.conf /opt/php-7.4.2/etc/php-fpm.d/
COPY php.ini /opt/etc/php/

EXPOSE 9000
CMD ["/opt/php-7.4.2/sbin/php-fpm", "--nodaemonize"]