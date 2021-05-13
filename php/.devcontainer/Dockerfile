FROM ubuntu:bionic
LABEL maintainer Brady Wetherington <uberbrady@gmail.com>

# No need to add `apt-get clean` here, reference:
# - https://github.com/snipe/snipe-it/pull/9201
# - https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#apt-get

RUN export DEBIAN_FRONTEND=noninteractive; \
    export DEBCONF_NONINTERACTIVE_SEEN=true; \
    echo 'tzdata tzdata/Areas select Etc' | debconf-set-selections; \
    echo 'tzdata tzdata/Zones/Etc select UTC' | debconf-set-selections; \
    apt-get update -qqy \
    && apt-get install -qqy --no-install-recommends \
    apt-utils \
    apache2 \
    apache2-bin \
    libapache2-mod-php7.2 \
    php7.2-curl \
    php7.2-ldap \
    php7.2-mysql \
    php7.2-gd \
    php7.2-xml \
    php7.2-mbstring \
    php7.2-zip \
    php7.2-bcmath \
    patch \
    curl \
    wget  \
    vim \
    git \
    cron \
    mysql-client \
    supervisor \
    cron \
    gcc \
    make \
    autoconf \
    libc-dev \
    pkg-config \
    libmcrypt-dev \
    php7.2-dev \
    ca-certificates \
    unzip \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


RUN curl -L -O https://github.com/pear/pearweb_phars/raw/master/go-pear.phar
RUN php go-pear.phar

RUN pecl install mcrypt-1.0.2

RUN bash -c "echo extension=/usr/lib/php/20170718/mcrypt.so > /etc/php/7.2/mods-available/mcrypt.ini"

RUN phpenmod mcrypt
RUN phpenmod gd
RUN phpenmod bcmath

RUN sed -i 's/variables_order = .*/variables_order = "EGPCS"/' /etc/php/7.2/apache2/php.ini
RUN sed -i 's/variables_order = .*/variables_order = "EGPCS"/' /etc/php/7.2/cli/php.ini