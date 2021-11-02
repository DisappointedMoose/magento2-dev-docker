FROM bitnami/php-fpm:7.4

RUN apt-get -y update \
	&& apt-get install -y \
	build-essential \
	autoconf \
	curl \
	wget \
	git \
	unzip \
	tar \
	bash-completion \
	&& apt-get clean

RUN cd / && \
	curl -O https://xdebug.org/files/xdebug-2.9.8.tgz && \
	tar -xzf xdebug-2.9.8.tgz && \
	cd xdebug-2.9.8 && \
	phpize && \
	./configure --enable-xdebug && \
	make && \
	make install

# Install Mhsendmail

RUN apt-get -y install golang-go \
	&& mkdir /opt/go \
	&& export GOPATH=/opt/go \
	&& go get github.com/mailhog/mhsendmail

# Install Magerun 2
RUN wget https://files.magerun.net/n98-magerun2.phar \
	&& chmod +x ./n98-magerun2.phar \
	&& mv ./n98-magerun2.phar /usr/local/bin/

# Install NPM + Grunt + Livereload
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - \
  	&& apt-get install -y nodejs build-essential \
    && curl https://raw.githubusercontent.com/creationix/nvm/v0.16.1/install.sh | sh \
    && npm i -g grunt-cli yarn

RUN npm i -g livereload

# update Composer
RUN composer self-update

# Configure
RUN mkdir /usr/sbin/.composer && \
	chmod -R 0777 /usr/sbin/.composer

RUN mkdir /usr/sbin/.npm && \
	chmod -R 0777 /usr/sbin/.npm

RUN groupadd -g 1000 hostusers
RUN groupadd -g 1001 hostusers2
RUN usermod -a -G 1000 daemon
RUN usermod -a -G 1001 daemon