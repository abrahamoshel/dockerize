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
