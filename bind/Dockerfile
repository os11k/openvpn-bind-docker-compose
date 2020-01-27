FROM debian:buster
RUN apt-get update -q && \
  apt-get -y upgrade && \
  DEBIAN_FRONTEND=noninteractive apt-get -y install bind9 && \
  sed -i '/options {/a\\tallow-recursion { localnets; localhost; };\n\tallow-query-cache { localnets; localhost; };\n\tallow-query { localnets; localhost; };\n' /etc/bind/named.conf.options && \
  rm -rf /var/lib/apt/lists/*
CMD ["/usr/sbin/named", "-c", "/etc/bind/named.conf", "-g"]
