FROM ubuntu:20.04

RUN \
    # Install Java 8
    apt update
    apt install openjdk-8-jdk

    # Install Riak
    && curl -fsSL "https://packagecloud.io/install/repositories/basho/riak/script.deb" > /tmp/riak_setup.sh \
    && chmod +x /tmp/riak_setup.sh && /tmp/riak_setup.sh \
    && apt-get install -y supervisor riak=2.0.5-1 \

    # Cleanup
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN locale-gen en_US en_US.UTF-8

COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY ./entrypoint.sh /
COPY ./ssl-cert /etc/riak

CMD ["/entrypoint.sh"]
