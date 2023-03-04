# Application Layer

This is the highest layer, which is on top of the transport layer. We will interact with the lower layers via the interface provided by the transport layer, which will mean (almost always) using a TCP socket or a UDP socket.

The protocols in this layer are application specific, so vary widely based on what the application is trying to do. Browser: HTTP; Email: SSH, SMTP

**Application** **topology**: client/server model = 2 programs behave different = HTTP; peer to peer model = all programs behave as both client and server = BitTorrent.

**Lower layers**: transport = process to process = port number to identify; network = host to host = IP address to identify. Clients = specify IP + port of server; Server = specify Port to listen on.

**Which transport layer protocol to use (in conflict):**

- Reliable data transfer: all data sent needs to be received in order; TCP
- Latency concerns: data needs to be received within a given time window; UDP
- Data rate concerns: data needs to be transmitted at a particular rate.

**HTTP**: text based, one-shot request/response model. TCP.

**SMTP**: Simple mail transfer protocol. Text based, mail sending protocol. Push system. TCP

**POP**: Post Office Protocol. To retrieve email. TCP

**BitTorrent**: Peer to peer protocol, sharing large files. “Tracker” servers kept track of and shared info about connected clients via HTTP. Switch from TCP to UDP (uTP = UDP torrent protocol)

**DNS** (Domain Name System): Makes the network layer work. IPv4 = 32 bits = 4 bytes. IPv6 = 128 bits = 8 * 16 bits. Answer “what’s the IP address for a domain name”. UDP.

The DNS system is hierarchical with the “root” which you can see by tracing a domain name (shell.cs.utah.edu) from right to left. The .edu is a “top level domain” (TLD) and utah.edu is a subdomain of it (cs.utah.edu a subdomain of that, etc). “Root” domains are responsible for knowing the IP addresses of all the TLD DNS servers.

**DNS Query Types:**

- A = give me the IP for a hostname
- NS = give me the name server for the hostname
- Type CNAME = give me the canonical name
- MX = tell me the canonical name of the email server for the domain.