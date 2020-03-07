FROM php:7.4-cli-buster

ARG HOST_UID=1000

RUN set -eux; \
# Create user
    adduser \
        --disabled-password \
        --gecos "Development User;"\
        --home /home/dev \
        --shell /bin/bash \
        --uid $HOST_UID \
        dev; \
    \
# Configure timezone
    ln -fs /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime ; \
# Install development packages
    apt-get update; \
    apt-get install -y --no-install-recommends \
        git \
        libmpc-dev \
        libpq-dev \
        libzip-dev \
        unzip \
        wget \
    ; \
# Install php extensions
    docker-php-ext-install \
        bcmath \
        ctype \
        gmp \
        iconv \
        json \
        pdo_pgsql \
        pgsql \
        zip \
    ; \
# Remove apt package list files
    rm -rf /var/lib/apt/lists/* ; \
# Install composer
    curl -sS https://getcomposer.org/installer \
        | php -- --install-dir=/usr/local/bin --filename=composer ; \
# Install symfony
    wget https://get.symfony.com/cli/installer -O - | bash ; \
    mv /root/.symfony/bin/symfony /usr/local/bin/symfony ; \
# Finish RUN command
    true ;

WORKDIR /app
