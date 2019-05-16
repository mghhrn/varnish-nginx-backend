# based on https://github.com/newsdev/docker-varnish
FROM debian:jessie

RUN \
  useradd -r -s /bin/false varnishd

# Install Varnish source build dependencies
RUN \
  apt-get update && apt-get install -y --no-install-recommends \
    automake \
    build-essential \
    autotools-dev \
    libedit-dev \
    libjemalloc-dev \
    libncurses-dev  \
    libpcre3-dev  \
    libtool  \
    pkg-config  \
    python-docutils  \
    python-sphinx  \
    graphviz \	
    git  \
    ca-certificates  \
    curl \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Install Varnish from source, so that Varnish modules
# can be compiled and installed
ENV VARNISH_VERSION=4.1.11

RUN  apt-get update && \
	  mkdir -p /usr/local/src && \
	  cd /usr/local/src && \
	  git clone -b 4.1 https://github.com/varnishcache/varnish-cache.git && \
	  cd varnish-cache && \
	  ./autogen.sh  && \
	  ./configure && \
	  make install
RUN 	  cd /usr/local/src && \
	  rm -r -f varnish-cache

# varnishd(1) options
ENV VARNISH_VCL_PATH /etc/varnish/default.vcl
ENV VARNISH_PORT 80
ENV VARNISH_MEMORY 64m
ENV VARNISH_TTL 60

# VMOD options
ENV QUERYSTRING_VERSION 0.3

# varnishlog(1) options
ENV VARNISHLOG_PATH /etc/varnish/log.log

# varnishncsa(1) options
ENV VARNISHNCSA_FORMAT_PATH /etc/varnishncsa/varnishncsa-format.txt
ENV VARNISHNCSA_LOG_PATH /var/log/varnish/access.log

COPY varnish/start-varnish.sh /usr/local/bin/start-varnish
COPY varnish/install-querystring.sh /usr/local/bin/install-querystring
COPY varnish/varnishncsa-format.txt /etc/varnishncsa/varnishncsa-format.txt

# install VMODs
RUN \
  install-querystring

# forward logs to docker log collector
RUN \
  mkdir -p $(dirname ${VARNISHNCSA_LOG_PATH}) && \
  mkdir -p $(dirname ${VARNISHLOG_PATH}) && \
  touch ${VARNISHLOG_PATH} ${VARNISHNCSA_LOG_PATH} && \
  ln -sf /dev/stdout ${VARNISHLOG_PATH} && \
  ln -sf /dev/stdout ${VARNISHNCSA_LOG_PATH}

EXPOSE 80
CMD [ "start-varnish" ]

ONBUILD COPY varnish/default.vcl /etc/varnish/default.vcl
