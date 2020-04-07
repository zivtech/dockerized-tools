FROM jenkins/jenkins:lts

ENV TERM xterm

USER root

# Update apt repos and install base apt packages.
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends apt-utils \
  apt-transport-https \
  build-essential \
  ca-certificates \
  curl \
  dirmngr \
  git \
  gnupg \
  less \
  lsb-release \
  nano \
  nodejs \
  software-properties-common \
  sudo \
  vim \
  wget \
  zip \
  && chown -R jenkins:jenkins /var/jenkins_home \
  && rm -rf /var/lib/apt/lists/*

## Install PHP and Composer.
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg \
  && echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" >> /etc/apt/sources.list.d/php7.3.list \
  && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends php7.3-cli \
  php7.3-curl \
  php7.3-xml \
  && curl -sS https://getcomposer.org/installer | php -- \
  --install-dir=/usr/local/bin \
  --filename=composer \
  && rm -rf /var/lib/apt/lists/*

# Install Terminus Pantheon command line tool, https://pantheon.io/docs/terminus.
RUN curl -O https://raw.githubusercontent.com/pantheon-systems/terminus-installer/master/builds/installer.phar \
  && php installer.phar install \
  && rm installer.phar

# Install WP-CLI Wordpress command line tool, https://wp-cli.org/.
RUN curl -o /tmp/wp-cli.phar https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
  && chmod +x /tmp/wp-cli.phar \
  && mv /tmp/wp-cli.phar /usr/local/bin/wp
