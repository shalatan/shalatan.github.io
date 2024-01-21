## System Design

## Client-Server Model

- `Client` : A machine or process that reuqests data or service from a server.
- `Server` : A machine or process that provides data or service for a client, usually by listening incoming calls.
- `Client-Server Model` : The paradigm by which modern systems are designed, which consists of clients requesting a data or service from server/s providing data or service.

### IP Address
An address given to each machine connected to public network.
IPv4: 4 numbers seperated by dots a.b.c.d.  
    - 127.0.0.1: localHost     
    - 192.168.x.y: private network

### Port
In order for multiple programs to listen to new network connections on same machine without colliding, they use a port to listen on. <br>
Ranges from 0 to 65535 (2^16)<br>
    - `0-1023`: system ports    
    - `22`: secures hell    
    - `53`: DNS     
    - `80`: HTTP    
    - `443`: HTTPS

### DNS
Short for Domain Name System, it describe the entities and protocols involved in translation from domain names to IP address

## Network Protocol

### IP
Stands for Internet Protocol. This protocol outlines how almost all machines-to-machines communication should happen in the world. Other protocols like TCP, UDP & HTTP are built on top of it.
- Less stoage capacity
- Inconsistent transfer of data
- Random order of tranfer of IP packets

### TCP
Stands for Transmission Control Protocl. Allows for ordered, reliable, data delivery between machines over the public internet by creating a connection. TCP is usually implemented in kernel, which exposes sockets to application that they can use to stream data through an open connnection.

### HTTP
The Hyper Text Transfer Protocol is a very common network protocol implemented on top of IP. Client makes a HTTP requests and server responds with a response.

## Storage