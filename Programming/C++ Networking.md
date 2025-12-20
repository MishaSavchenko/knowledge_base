---
tags:
  - old_docs
  - cpp
  - programming
---

# Networking Programming 

Refs: [Beej’s Guide to Network Programing](https://beej.us/guide/bgnet/)

# Sockets

* A way to speak to other programs using standard Unix file descriptors  
* Unix programs do I/O by reading/writing to a file descriptor (integer associated with an open file), this file descriptor can be pipe, network connection, a FIFO, on-the-disk fil, etc.   
* socket()   
  * Calling socket() system routine return socket descriptor allowing to use it via send() recv(). read() and write() can also be used by do not allow greater control over data transmission like send()/recv()  
* Type of sockets   
  * Row Sockets (\*)  
  * Stream Sockets   
    * SOCK\_STREAM  
    * Reliable two way connected communication streams   
    * Practically error-free   
    * **telnet** applications  
    * HTTP protocol uses stream sockets to get pages   
    * Use transmission control protocol, TCP (\*)  
      * Makes sure that data arrives sequentially and error-free   
    * Stream sockets us IP(\*) for data routing   
  * Datagram Sockets (connectionless sockets)  
    * SOCK\_DATAGRAM  
    * May arrive, may arrive out of order   
    * If it arrives the data within the packet will be error free  
    * Datagram sockets also use IP for data routing   
    * Use  user datagram protcol, UDP   
    * Connectionless because they do not have to maintain an open connection as you do with stream sockets   
      * Build a packet, add the IP header and send it out, without the necessary part of making a connection   
    * Used when tcp isnt available or when few dropped packets arent necessary   
      * Trivial file tranfer protcol (tftp)(\*)  
      * DHCP client (dhcpcd) (\*)  
      * Multiplayer games  
      * Streaming audio   
      * Video conferencing   
    *  Whie tftp and dhcpcd are used to transfer binary applications from one host to another they have their own protocols on top of UDP that send back ACK (aakwnoladgment packet). If the sender of the originial packet rcives no reply it will try to transmit the packet until the reply is recieved again   
      * ACK procedure is very important when constructing SOCK\_DGRAM  
    * Faster than tcp   
  * Network Theory   
    * Data Encapsulation   
      * Data packet is wrapped within a first protocol header (and maybe a footer), which is then wrapped in with the second protocol, and then a third and then with final protocol on the hardware   
      * EX. \[ Ethernet \[ IP \[ UDP \[ TFTP \[ Data \] \] \] \]  
      * When another computer receives the pakcet the hardware strips the packets in reverse   
      * EX: Hardware strips Ethernet header, Kernel strips IP, then UDP, TFTP program strips TFTP header and the data is recieved   
    * Layered Network Model (ISO/OSI)  
      * Descrives a ssystem of network functionality that has many advantages over other models   
      * I.e. sockets writing can be done without caring how the data is physically transmitted because programs on the lower level deal with it for you   
      * Model   
        * Appication   
          * Place where users interact with the network  
        * Presentation   
        * Session   
        * Transport   
        * Network   
        * Data Link  
        * Physical   
          * Hardware: serial, ethernet, etc.   
      * Unix Model   
        * Application Layer (telnet, ftp, etc)  
        * Host-to-host transport layer (UDP, TCP)  
        * Internet layer (IP and routing)   
        * Network access layer (Ethernet, wi-fi, whatever)   
      * send() for stream socket and sendto() for datagram socket is all you need in order to encapsulate the data   
      * Kernel builds the transport and internet layer and the hardware does network access layer 

# IP Addresses, structs, and Data Munging 

## IP Addresses (pg 16 stop) 

* Network routing system   
* IPv4   
  * Older network routing system   
  * Addresses made up of four bytes (four octets)   
  * 192.0.2.111 (number and dots look)   
  * Virtually every site on the internet uses IPv4  
  * 127.0.0.1 is a loopback address   
  * To express the IPv4 address as IPv6   
    * 192.0.2.33 \=\> ::ffff:192.0.2.33  
* IPv6  
  * 79 million billion trillion times as many possible address as IPv4   
  * 2001:0db8:c9d2:aee5:73e3:934a:a5ae:9551 ( hexadecimal representation )  
    * Compression of these addresses when there are a lot of zeros is also available   
    * 2001:0db8:c9d2:0012:0000:0000:0000:0051  
      * 2001:db8:c9d2:12::51  
    * 2001:0db8:ab00:0000:0000:0000:0000:0000  
      * 2001:db8:ab00::  
    * 0000:0000:0000:0000:0000:0000:0000:0001  
    * ::1  
  * ::1 is loopback address (this machine im running on nuw)   
* Subnets	  
  * Network protion and host  portion of IP addresses  
  * 192.0.2.12  
    * 192 \-\> network portion   
    * 12 \-\> host portion  
  * Network portion (netmask)  
    * Bitwise AND with the IP adress to get network number out of it   
    *   
    * Netmask is usually 255.255.255.0  
      * 255.255.255.0  AND 192.0.2.12 \=\> 192.0.2.12  
    * Currently netmask is arbitrary number of bits  
    * New style of netmask   
      * IPv4 192.0.2.12/30  
      * IPv6 2001:db8::/32 or 2001:db8:5413:4028::9db9/64   
* Port Numbers   
  * 16 bit number that like a local address for the connections   
  * Used by UDP and TCP   
* Byte Order   
  * Computers sometimes store bytes in reverse order Little-Endian storage   
  * Big-Endian or Network Byte Order   
    * Network type like this storage   
  * Computers store numbers in Host Byte Order which might be Little-Endian or Big-Endian depending on hardware   
  * Always sett the packets to Network Byte Order   
  * Two types of number that can be converted to network byte order   
    * Short (two byte)   
    * Long (four bytes)    
  * Converting functions   
    * Can be “assembled”  
    * I.e. short from host byte order to netwrok byte order   
    * h for host \+ to \+ n for network \+ s for short   
    * htons() (Host to Network Short)   
    * Combinations of   
      * n :network  
      * h :host  
      * l :long   
      * s :short   
* structs   
  * Socket descriptions are of the type int   
  * **struct addrinfo** { … }  
    * Used to prep socket address structures for subsequent use   
    * Used in host name and service name lookups   
    * Load struct up with the necessary data and call **getaddrinfo()**  
    * **getaddrinfo()** returns a pointer to new linked list of sturctures filled out with the info you need   
      * Usually fills out the **struct addrinfo**  
    * **ai\_family** field can designated whether to use IPv4 or IPv6 or **AF\_UNSPEC** for use whatever   
      * This allows for the code to be IP agnostic   
    * **ai\_next** points at the next element (\*)   
      *   
    * **ai\_addr** field is a pointer to a **struct sockaddr**  
  * **struct sockaddr { … }**   
    * Holds address information for many types of sockets   
    * Parallel **struct sockaddr\_in**   
      * Can be cast to a pointer to a **struct sockaddr** and vice versa   
      * **connect()** wants **struct sockaddr\***  but both can be used   
    * **sin\_zero** field in **sockaddr\_in** should be set to all zeros with the function **memset()**  
    * **sin\_family** field corresponds to **sa\_family** in a **sockaddr** and should be set to **AF\_NET**   
    * **sin\_port** must be in NEtwork Byte Order   
    * d

IP  
Routing   
Tftp   
Dhcpcd  
Telnet   
HTTP 