FROM ubuntu:20.04
ENV DEBIAN_FRONTEND noninteractive
##update packages
RUN apt-get update -y && apt-get upgrade -y
#
##install packages
#RUN apt-get install -y openssh-server
RUN apt-get install -y php
RUN apt-get install -y libapache2-mod-php
RUN apt-get install -y curl
RUN apt-get install -y nano
RUN apt-get install -y php-tokenizer
RUN apt-get install php-bcmath -y
RUN apt-get install php-mbstring -y
RUN apt-get install zip -y
RUN apt install php-curl -y
RUN apt install php-mysql -y

#dev stuff
RUN apt install php-pear -y
RUN apt install php-dev -y
RUN pecl install xdebug


COPY ./docker/000-default.conf /etc/apache2/sites-enabled/
COPY ./docker/php.ini /etc/php/7.4/apache2/

COPY . /var/www/html

#
## install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#
##enable apache mods
#RUN a2enmod php
RUN a2enmod rewrite
#
## awslog agent to push access and error logs to cloudwatch
#ADD docker/awslogs.conf /var/awslogs/etc/_awslogs.conf
#RUN wget https://s3.amazonaws.com/aws-cloudwatch/downloads/latest/awslogs-agent-setup.py
#RUN python ./awslogs-agent-setup.py --region eu-west-1 --non-interactive --configfile=/var/awslogs/etc/_awslogs.conf
#
##expose ports needed
EXPOSE 80
#
## Update the default php.ini with the config we created.
#ADD docker/php.ini /etc/php5/apache2/php.ini
#ADD docker/php.ini /etc/php5/cli/php.ini


CMD ["apachectl", "-D" , "FOREGROUND"]
