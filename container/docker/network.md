# Docker Networking

Network drive: Build-in or 3rd party extension that provides virtual network features.

Different Types of network drive:

1. Bridge
2. Host
3. None
4. Overlay
5. IPVlan
6. macVlan

* Each container while starting is assigned to a private virtual network by default "bridge".By default, while creating or running a container using docker create or docker run, the container doesn’t expose any of its ports to the outside world.
* Each virtual network routes through NAT firewall on host.
* All containers on a virtual network can talk to each other without port forwarding (using -p).
* As one device can be attached to multiple networks. One container can be connected to more than one virtual private network and obviously vise-versa one private network can have multiple containers.
* The containers can also be connected to the host network by using the host network type (--net=host).
* Bridge network drive: Simple built-in driver that creates a local virtual network with its own subnet starting with 172.17.0.0 and above 172.18.0.0 .

## IP address and hostname

By default, the container gets an IP address for every Docker network it attaches to. A container receives an IP address out of the IP pool of the network it attaches to. The Docker daemon effectively acts as a DHCP server for each container. Each network also has a default subnet mask and gateway.

A container’s hostname defaults to be the container’s ID in Docker, making the containers in the same network to communicate with the hostname.

### Docker Networks: DNS

* Docker daemon has a built-in DNS server that containers uses by default.
* By default, containers inherit the DNS settings of the host, as defined in the /etc/resolv.conf configuration file. Containers that attach to the default bridge network receive a copy of this file. Containers that attach to a custom network use Docker’s embedded DNS server. The embedded DNS server forwards external DNS lookups to the DNS servers configured on the host.

---

## Links

* <https://docs.docker.com/config/containers/container-networking/>