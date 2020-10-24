ARG WP_VERSION=php7.4-fpm
FROM wordpress:${WP_VERSION}


######################################
# USE MAILHOG
# Capture emails and send it to mailhog
# INSTALL GO and configure mhsendmail to send to maihlog path
######################################
ARG USE_MAILHOG=false
ARG MAILHOG_PORT=1025
# INSTALL GO
RUN if [ ${USE_MAILHOG} = true ]; then \
  apt-get update \
    && apt-get install --no-install-recommends -y ca-certificates curl git nano \
    && rm -rf /var/lib/apt/lists/* \
    && curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf - \
;fi

# CONFIGURE mhsendmail
ENV PATH /usr/local/go/bin:$PATH
RUN if [ ${USE_MAILHOG} = true ]; then \
go get github.com/mailhog/mhsendmail \
  && cp /root/go/bin/mhsendmail /usr/local/bin/mhsendmail \
  && echo "sendmail_path = /usr/local/bin/mhsendmail --smtp-addr mailhog:${MAILHOG_PORT}" > /usr/local/etc/php/conf.d/sendmail.ini \
;fi