FROM nginx:1.9.6
MAINTAINER Donal Byrne <byrnedo@tcd.ie>

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update -qq && \
    apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    runit \
    unzip && \
    rm -rf /var/lib/apt/lists/*

ENV CT_URL https://releases.hashicorp.com/consul-template/0.12.0/consul-template_0.12.0_linux_amd64.zip
RUN curl -L $CT_URL > /tmp/ct.zip && unzip /tmp/ct.zip -d /usr/local/bin

ADD nginx.service /etc/service/nginx/run
ADD consul-template.service /etc/service/consul-template/run

RUN rm -v /etc/nginx/conf.d/*
ADD nginx.conf /etc/consul-templates/nginx.conf

VOLUME ["/etc/nginx/certs"]

CMD ["/usr/bin/runsvdir", "/etc/service"]
