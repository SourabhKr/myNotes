# What is a port?

A port is not a physical connection, it's a logical connection, that's used by programmes ans services to exchange information. It is used to determine which service/programme will be used to process the information (request/data).

The port numbers are unique and ranges from:  0  - 65535

The common port numbers are:  

* 80, 443 - Web pages (HTTP, HTTPS)
* 21 - FTP (File Transfer Protocol)
* 25 - Email (SMTP)

A port number is always associated with an IP address, in a nutshell an IP address is used to determine the exact location of a server, whereas the port number determines which application/programme will process the request.

Port number are divided into three main categories:

1. 0 - 1023 : System/ Wellknown ports. Ex: 80 : HTTP, 21 - FTP
2. 1024 - 4915: User/Registered ports(can be registered by a user or a company for a particular service.) Ex: 1102: Adobe Server, 1433: MicroSoft SQL Server.
3. 49152 - 65535 : Dynamic/Private ports (Client side ports used by different services/programmes running locally during a session to operate properly)

Out of the above-mentioned: 1 and 2 are basically used by servers and 3 is used the local computer.

Note: Servers don't always mean a physically distant system, the local system can also act as a server for other services in the same system or for an external device in a network. So the ports mentioned in category 1, can still be used by the local system.

![Port Mapping Example](/asset/images/networking/port_mapping_example.png)

In the above example the dynamic ports are assigned by the local computer seen as Local address which is used to map, which request should be processed by which service in the local computer.

---

## Links

* <https://www.youtube.com/watch?v=g2fT-g9PX9o>