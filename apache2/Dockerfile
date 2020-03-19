FROM ubuntu
ENV TZ=Europe/Amsterdam
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt-get update -y && apt-get install -y apache2 apache2-utils php php-mysql php-xml php-json php-zip libapache2-mod-php wget git
ADD apache2.conf /etc/apache2/apache2.conf
ADD ports.conf /etc/apache2/ports.conf
ADD 000-default.conf /etc/apache2/sites-available/000-default.conf
RUN groupadd -g 1000 webserver
RUN useradd -rm -u 1000 -g webserver webserver
RUN chown -R webserver:webserver /var/log/apache2 /var/www/html /var/run/apache2
RUN wget -P /tmp https://getcomposer.org/composer.phar && mv /tmp/composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer
USER webserver:webserver
WORKDIR /var/www/html/
EXPOSE 8080
CMD [ "apache2ctl", "-D", "FOREGROUND" ]
