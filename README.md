openvpn-bind-docker-compose
==============

OpenVPN server in a Docker with separate Bind server, so no DNS leak happens.

## Quick Start VPN server.
### !!!Please do not use Ubuntu as host server, because it is using 53 port what is needed for BIND. I recommend using Debian Buster!!!

* Install docker-compose on your server and clone git repository

```
apt-get update && apt-get upgrade -y && apt-get install docker-compose dnsutils -y
mkdir /docker && cd /docker
git clone https://github.com/os11k/openvpn-bind-docker-compose.git
cd ./openvpn-bind-docker-compose/
```

* Start OpenVPN and BIND containers

```
docker-compose up -d --build
```

* Generate a client certificate without a passphrase

```
docker exec openvpn easyrsa build-client-full CLIENTNAME nopass
```

* Retrieve the client configuration with embedded certificates

```
docker exec openvpn ovpn_getclient CLIENTNAME tcp $(echo $(dig -4 +short myip.opendns.com @resolver1.opendns.com)) 443 > CLIENTNAME.ovpn
```

* Revoke the client certificate

```
docker exec openvpn ovpn_revoke CLIENTNAME
```

## Credits

* https://github.com/tsaikd/docker-openvpn
* https://github.com/tomav/docker-bind
