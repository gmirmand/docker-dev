FROM wearepvtl/php-fpm-5.6

LABEL maintainer.name="Pivotal Agency" \
      maintainer.email="tech@pvtl.io"

RUN if [ ${CUSTOM_USER_ID:-0} -ne 0 ] && [ ${CUSTOM_GROUP_ID:-0} -ne 0 ]; then \
    userdel -f www-data &&\
    if getent group www-data ; then groupdel www-data; fi &&\
    groupadd -g ${CUSTOM_GROUP_ID} www-data &&\
    useradd -l -u ${CUSTOM_USER_ID} -g www-data www-data \
;fi

# Run the user specified commands
ARG EXTRA_CMDS="echo 'None to run'"
RUN eval $EXTRA_CMDS

# Custom PHP.ini Config
COPY ./conf/custom.ini /usr/local/etc/php/conf.d/zzb-custom.ini

# CRON's (if they exist)
COPY ./56/Dockerfile ./56/custom_crontab* /root/

ENTRYPOINT []
CMD ["/usr/bin/supervisord"]
