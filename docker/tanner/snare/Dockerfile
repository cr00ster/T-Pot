FROM alpine:3.14
#
# Include dist
ADD dist/ /root/dist/
#
# Setup apt
RUN apk -U --no-cache add \
               build-base \
               git \
               linux-headers \
               python3 \
               python3-dev \ 
               py3-pip && \ 
#
# Setup Snare 
    git clone https://github.com/mushorg/snare /opt/snare && \
    cd /opt/snare/ && \
    git checkout 0919a80838eb0823a3b7029b0264628ee0a36211 && \
    pip3 install --no-cache-dir setuptools && \
    pip3 install --no-cache-dir -r requirements.txt && \
    python3 setup.py install && \
    cd / && \
    rm -rf /opt/snare && \
    mkdir -p /opt/snare/pages && \
#    clone --target http://example.com && \
    mv /root/dist/pages/* /opt/snare/pages/ && \
#   
# Clean up
    apk del --purge \
            build-base \
            linux-headers \
            python3-dev && \
    rm -rf /root/* && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/cache/apk/*
#
# Start snare
STOPSIGNAL SIGKILL
CMD snare --tanner tanner --debug true --no-dorks true --auto-update false --host-ip 0.0.0.0 --port 80 --page-dir $(shuf -i 1-10 -n 1)
