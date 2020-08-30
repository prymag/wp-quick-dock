ARG WP_VERSION=php7.4-fpm
FROM wordpress:${WP_VERSION}

######################################
# INSTALL mhsendmail
# for sending email to mailhog
######################################

# INSTALL GO
RUN apt-get update \
  && apt-get install --no-install-recommends -y ca-certificates curl git nano \
  && rm -rf /var/lib/apt/lists/* \
  && curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -

# CONFIGURE mhsendmail
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail \
  && cp /root/go/bin/mhsendmail /usr/local/bin/mhsendmail \
  && echo "sendmail_path = /usr/local/bin/mhsendmail --smtp-addr mailhog:1025" > /usr/local/etc/php/conf.d/sendmail.ini

########## END INSTALL mhsendmail ################