FROM redis:6.2.6-alpine3.14
#
# Include dist
ADD dist/ /root/dist/
#
# Setup apt
RUN apk -U --no-cache add redis && \ 
    cp /root/dist/redis.conf /etc && \
#
# Clean up
    rm -rf /root/* && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/cache/apk/*
#
# Start redis
STOPSIGNAL SIGKILL
USER nobody:nobody
CMD redis-server /etc/redis.conf
