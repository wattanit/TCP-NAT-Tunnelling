# TCP-NAT-Tunnelling

Perform TCP tunnelling to a host behind NAT layer/firewall through the use of a public gateway server.

## Terminology

**service host (agent)** - host that provides web services, in this case the service host is placed behind NAT layers. For example, a PC running in a home network.

**Gateway host** - host that provides reverse tunnelling which is placed in a public network (has public IP address). For example, a cloud instance.

## Concept

The basic concept is as follows:
1. The gateway host is running on a public internet such as cloud service, and can be connected to from everywhere.
2. The service host cannot be connected to directly as it lives behind a NAT layer. However, the service host can connect to and establish a websocket with the gateway host.
3. The gateway host then forward any incomming traffics to the service host via the established websocket, i.e., the gateway host acts as a proxy.

## Requirements

1. Both gateway host and service host have Docker and Docker-compose installed.
2. Gateway host is accessible from the internet, preferably has a static IP address.

## Quick starts

1. On the Gateway host, clone this repository.
2. Open gateway/docker-compose.yml to change the configuration. In particular the following variable should be changed: 
   - ports : list of all ports to be forwarded to service host, as well as the RTUN_PORT itself.
   - RTUN_AGENTS: list of all port and protocols to be forwarded, and a key for each service host.
3. run ```docker-compose up -d``` inside the gateway directory.
4. On the Service host, clone this repository.
5. Open agent/docker-compose.yml to change the configuration. In particular the following variables should be changed:
   - RTUN_GATEWAY : address to the Gateway host e.g. ```ws://<gateway-ip>:9000```
   - RTUN_KEY : key for this service host as specified in the gateway
   - RTUN_FORWARD : list of all port and protocols to be handled. 
 6. run ```docker-compose up -d``` inside the agent directory.

## Documentation
More information on https://github.com/snsinfu/reverse-tunnel/blob/master/docker/README.md
