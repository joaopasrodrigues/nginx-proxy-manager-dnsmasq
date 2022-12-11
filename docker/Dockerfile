# This is a Dockerfile intended to be built using `docker buildx`
# for multi-arch support. Building with `docker build` may have unexpected results.

# This file assumes that the frontend has been built using ./scripts/frontend-build

FROM  jc21/nginx-proxy-manager:latest

WORKDIR /
RUN apt-get update
RUN apt-get -y install dnsmasq
RUN mkdir -p /etc/services.d/dnsmasq
COPY run /etc/services.d/dnsmasq
RUN ln -s /bin/true /etc/services.d/dnsmasq/finish 
RUN chmod +x /etc/services.d/dnsmasq/*

WORKDIR /etc/services.d/nginx/

RUN head -n -1 run >> run.tmp
RUN echo "sed -i 's/127.0.0.11/127.0.0.1/g'  /etc/nginx/conf.d/include/resolvers.conf" >> run.tmp
RUN tail -1 run >> run.tmp
RUN mv run run.orig 
RUN mv run.tmp run
RUN chmod +x run


WORKDIR /


