FROM ubuntu:16.04

    RUN apt-get update && apt-get upgrade -y
    # Install Java 8
    RUN sed -i.bak 's/main$/main universe/' /etc/apt/sources.list 
    RUN apt-get update -qq 
    RUN apt-get install -y apt-utils
    RUN apt-get install -y software-properties-common 
    RUN apt-get install -y curl
    RUN apt-get install -y openjdk-8-jdk openjdk-8-jre 
    # Install Riak
    RUN curl -s https://packagecloud.io/gpg.key | apt-key add -
    RUN apt-get install -y apt-transport-https
    RUN curl "https://packagecloud.io/install/repositories/basho/riak/config_file.list?os=ubuntu&dist=trusty&name=gurosh" > /etc/apt/sources.list.d/basho.list
    # RUN curl -fsSL "https://packagecloud.io/install/repositories/basho/riak/script.deb" > /tmp/riak_setup.sh 
    # RUN chmod +x /tmp/riak_setup.sh 
    # RUN /tmp/riak_setup.sh 
    RUN apt-get install -y supervisor 
    RUN apt-get -s update
    RUN apt-get install -y riak 
    # Cleanup
    # RUN apt-get clean 
    # RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN locale-gen en_US en_US.UTF-8

COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY ./entrypoint.sh /
COPY ./ssl-cert /etc/riak

CMD ["/entrypoint.sh"]
