FROM ubuntu:18.04
# Install Riak from packagecloud
# RUN \
#     sed -i.bak 's/main$/main universe/' /etc/apt/sources.list \
#     && apt-get update -qq && apt-get install -y software-properties-common curl vim ssh \
#     && apt-add-repository ppa:openjdk-r/ppa -y && apt-get update -qq \
#     && apt-get install -y openjdk-8-jdk \
#     && curl -fsSL "https://packagecloud.io/install/repositories/basho/riak/script.deb" > /tmp/riak_setup.sh \
#     && chmod +x /tmp/riak_setup.sh && ./tmp/riak_setup.sh \
#     && apt-get update && apt-get install -y supervisor riak \
#     && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#Installing Erlang
RUN apt-get install build-essential autoconf libncurses5-dev openssl libssl-dev fop xsltproc unixodbc-dev git \
    && apt-get install libwxbase2.8 libwxgtk2.8-dev libqt4-opengl-dev wget \
    && wget http://s3.amazonaws.com/downloads.riak.com/erlang/otp_src_R16B02-basho10.tar.gz \
    && tar zxvf otp_src_R16B02-basho10.tar.gz \
    && cd OTP_R16B02_basho10 \
    && ./otp_build autoconf \
    && ./configure && make && sudo make install \
    && erl \
    && cd ..
#Install Riak from AWS
RUN \
    apt-get update -qq && apt-get install -y build-essential libc6-dev-i386 git \
    && apt-add-repository ppa:openjdk-r/ppa -y && apt-get update -qq \
    && apt-get install -y openjdk-8-jdk \
    && wget http://s3.amazonaws.com/downloads.riak.com/riak/2.2/2.2.3/riak-2.2.3.tar.gz \
    && tar zxvf riak-2.2.3.tar.gz \
    && cd riak-2.2.3 \
    &&make rel

RUN locale-gen en_US en_US.UTF-8

COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY ./entrypoint.sh /
COPY ./ssl-cert /etc/riak

CMD ["/entrypoint.sh"]
