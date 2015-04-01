# Dockerfile for a Rails application using Nginx and Unicorn

# Select ubuntu as the base image
FROM ubuntu:15.04

MAINTAINER Abraham Oshel <abraham.oshel@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# Install common dependancies for ruby and go
RUN apt-get update -qq
RUN apt-get install -y \
      apt-utils \
      curl \
      autoconf
RUN apt-get install -y \
      build-essential \
      gcc \
      git \
      libc6-dev \
      libcurl4-openssl-dev \
      libevent-dev \
      libffi-dev \
      libmysqlclient-dev \
      libpq-dev \
      libqt4-dev \
      libreadline-dev \
      libsqlite3-dev \
      libssl-dev \
      libxml2-dev \
      libxslt-dev \
      libyaml-dev \
      make \
      ntp \
      openssl \
      vim \
      zlib1g \
      zlib1g-dev --fix-missing --no-install-recommends
      ## Perhaps for Production Builds
      # libreadline6 \
      # libreadline6-dev \
      # imagemagick \
      # pip

# Download go src into /usr/src
ENV GOLANG_VERSION 1.4.2
RUN curl -sSL https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz \
    | tar -v -C /usr/src -xz

# Run make on go src
RUN cd /usr/src/go/src && \
    ./make.bash --no-clean 2>&1

# Add go to PATH
ENV PATH /usr/src/go/bin:$PATH

# Setup Go enviroment
RUN mkdir -p /opt/go/src /opt/go/bin && \
    chmod -R 775 /opt/go
ENV GOPATH /opt/go
ENV PATH /opt/go/bin:$PATH

# Install ruby
ENV RUBY_MAJOR 2.1
ENV RUBY_VERSION 2.1.5
RUN mkdir -p \
    /usr/src/ruby \
    && curl -SL "http://cache.ruby-lang.org/pub/ruby/$RUBY_MAJOR/ruby-$RUBY_VERSION.tar.bz2" \
      | tar -xjC /usr/src/ruby --strip-components=1 && \
    cd /usr/src/ruby \
    && autoconf \
    && ./configure --disable-install-doc \
    && make install \
    && apt-get purge -y --auto-remove bison libgdbm-dev ruby \
    && rm -r /usr/src/ruby

# Add rails project to project directory
# ADD . /opt/app

# set WORKDIR
# WORKDIR /opt/app

RUN echo 'gem: --no-rdoc --no-ri' >> "$HOME/.gemrc"
RUN gem update --system

ENV GEM_HOME /usr/local/bundle
ENV PATH $GEM_HOME/bin:$PATH
RUN gem install \
  bundler \
  && bundle config --global path "$GEM_HOME" \
  && bundle config --global bin "$GEM_HOME/bin"

# don't create ".bundle" in all our apps
ENV BUNDLE_APP_CONFIG $GEM_HOME

# CMD '/bin/bash'
