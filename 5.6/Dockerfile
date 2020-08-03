FROM debian:jessie

MAINTAINER Jindrich Skupa <jindrich.skupa@gmail.com>

# Timezone
ENV TZ=Europe/Prague

RUN \
  apt-get update && \
  apt-get install -y \
  wget gnupg apt-transport-https curl && \
  apt-get autoremove -y && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists 

RUN echo "deb https://deb.nodesource.com/node_11.x jessie main" > /etc/apt/sources.list.d/nodesource.list && \
  echo "deb-src https://deb.nodesource.com/node_11.x jessie main" >> /etc/apt/sources.list.d/nodesource.list && \
  wget -qO- https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
  sed -i 's/deb.debian.org/archive.debian.org/g' /etc/apt/sources.list && \
  sed -i '/jessie-updates/d' /etc/apt/sources.list && \
  wget -qO- https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | bash

RUN \
  apt-get update && \
  apt-get install -y \
    curl \
    unzip \
    vim \
    git \
    apt-transport-https \
    locales \
    iptables \
    apache2 \
    php5 \
    php5-mysql \
    php5-mcrypt \
    php5-gd \
    php5-memcache \
    php5-curl \
    php-pear \
    php5-apcu \
    php5-pgsql \
    php5-soap \
    php5-cli \
    php5-curl \
    php5-mcrypt \
    php5-sqlite \
    php5-intl \
    php5-tidy \
    php5-imap \
    php5-json \
    php5-imagick \
    php5-common \
    php5-phalcon \
    libapache2-mod-php5 \
    libapache2-mod-rpaf \
    nodejs && \
  a2enmod proxy && \
  a2enmod proxy_http && \
  a2enmod alias && \
  a2enmod dir && \
  a2enmod env && \
  a2enmod mime && \
  a2enmod reqtimeout && \
  a2enmod rewrite && \
  a2enmod status && \
  a2enmod filter && \
  a2enmod deflate && \
  a2enmod setenvif && \
  a2enmod vhost_alias && \
  a2enmod ssl && \
  a2enmod php5 && \
  apt-get autoremove -y && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
  npm install bower -g

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
  && dpkg-reconfigure --frontend noninteractive tzdata \
  && echo 'en_US.UTF-8 UTF-8\ncs_CZ.UTF-8 UTF-8\n' >> /etc/locale.gen \
  && /usr/sbin/locale-gen

RUN ln -sf /dev/stderr /var/log/apache2/error.log

EXPOSE 80
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

