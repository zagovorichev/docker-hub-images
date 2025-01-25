FROM jenkins/ssh-agent

RUN apt update && apt install -y git zip unzip  build-essential \
    wget curl gnupg python3 make \
    lsb-release ca-certificates apt-transport-https software-properties-common

# PHP
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/sury-php.list
RUN wget -qO - https://packages.sury.org/php/apt.gpg | apt-key add -

# Node + Yarn
RUN curl -sL https://deb.nodesource.com/setup_22.x -o /tmp/nodesource_setup.sh \
    && bash /tmp/nodesource_setup.sh \
    && rm /tmp/nodesource_setup.sh

# Install packages
# pdo to run unit tests with sqlite
RUN apt update && apt install -y php8.4 php8.4-curl php8.4-xml php8.4-mbstring php8.4-pdo php8.4-sqlite3 php8.4-gd php8.4-zip php8.4-imagick \
    && apt-get install --quiet --yes --no-install-recommends nodejs \
    && npm install yarn --global \
    && npm install -g bower \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Composer
RUN curl -ksS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

RUN rm -rf /var/www/html \
    && chmod 0777 /tmp/

