# TCP-NAT-Tunnelling

Perform TCP tunnelling to a host behind NAT layer/firewall through the use of a public gateway server.

## Terminology

**service host** - host that provides web services, in this case the service host is placed behind NAT layers. For example, a PC running in a home network.

**Gateway host** - host that provides reverse tunnelling which is placed in a public network (has public IP address). For example, a cloud instance.

## Concept

The basic concept is as follows:
1. The gateway host is running on a public internet such as cloud service, and can be connected to from everywhere.
2. The service host cannot be connected to directly as it lives behind a NAT layer. However, the service host can connect to and establish a websocket with the gateway host.
3. The gateway host then forward any incomming traffics to the service host via the established websocket, i.e., the gateway host acts as a proxy.

## Requirements

1. Both gateway host and service host have Docker and Docker-compose installed.
2. Gateway host is accessible from the internet, preferably has a static IP address.
