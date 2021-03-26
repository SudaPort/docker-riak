FROM ubuntu:18.04

    RUN apt-get update && apt-get upgrade -y
    # Install Java 8
    RUN sed -i.bak 's/main$/main universe/' /etc/apt/sources.list 
    RUN apt-get update -qq 
    RUN apt-get install -y software-properties-common 
    RUN apt-get install -y curl
    RUN add-apt-repository ppa:webupd8team/java -y 
    RUN apt-get update -qq 
    RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections 
    RUN apt-get install -y oracle-java8-set-default 
    # Install Riak
    RUN curl -fsSL "https://packagecloud.io/install/repositories/basho/riak/script.deb" > /tmp/riak_setup.sh 
    RUN chmod +x /tmp/riak_setup.sh RUN /tmp/riak_setup.sh 
    RUN apt-get install -y supervisor riak=2.0.5-1 
    # Cleanup
    RUN apt-get clean RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN locale-gen en_US en_US.UTF-8

COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY ./entrypoint.sh /
COPY ./ssl-cert /etc/riak

CMD ["/entrypoint.sh"]
