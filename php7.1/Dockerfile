FROM debian:unstable
ENV DEBIAN_FRONTEND="noninteractive"
RUN apt-get update -yqq && apt-get upgrade -yqq
RUN apt-get -yqq install wkhtmltopdf default-mysql-client wget unzip findutils make git
RUN apt-get -yqq install php7.1-cli php7.1-gd php7.1-pdo php7.1-mbstring php7.1-dom php7.1-curl php7.1-xml php7.1-mysql php7.1-dev
# le paquet php-xdebug a une dépendance vers PHP7.2. Pour PHP7.1 on ne peut pas faire un simple apt install php-xdebug
RUN wget -O xdebug-2.6.1.tgz http://xdebug.org/files/xdebug-2.6.1.tgz && tar -xvzf xdebug-2.6.1.tgz && cd xdebug-2.6.1 && phpize && ./configure && make && cp modules/xdebug.so /usr/lib/php/20160303 && echo 'zend_extension = /usr/lib/php/20160303/xdebug.so' >> /etc/php/7.1/cli/php.ini
RUN apt-get -yqq install composer php-pear librdkafka-dev
#RUN pecl update-channels
RUN pecl install rdkafka
# Attention... En PHP 7.2, on enlève le .so et on laisse juste rdkafka
RUN echo 'extension=rdkafka.so' >> /etc/php/7.1/cli/php.ini
RUN wget -O /usr/local/bin/phpmetrics https://github.com/phpmetrics/PhpMetrics/releases/download/v2.4.1/phpmetrics.phar && chmod +x /usr/local/bin/phpmetrics
RUN wget -O /usr/local/bin/phpunit https://phar.phpunit.de/phpunit-7.phar && chmod +x /usr/local/bin/phpunit
RUN wget -O /usr/local/bin/phpcov https://phar.phpunit.de/phpcov.phar && chmod +x /usr/local/bin/phpcov
RUN apt-get -yqq install php-apcu
