# Network

**Network**: A network of networks that allows “hosts” to communicate with each other

**Host**: Hosts are endpoints that want to exchange data. Clients initiate connections with servers (clients and servers are both hosts). Hosts can be any sort of physical device: phone, laptop, desktop, smart fridge, “server” (typically rack mounted, powerful computer)

**Protocol**: A protocol is a precise set of rules for communication specifying data formats, who talks when, etc.

**Network Layer Model:**

- Application layer: application specific, depends on what you're trying to do. Common protocols are HTTP, DNS, SSH, SMTP, IMAP; human-computer interaction layer, app can access network services.
- Transport Layer: Process to process communication on networked hosts. TCP, UDP, and sort of QUIC; transmit data using transmission protocols.
- Network Layer: Host to Host communication: pretty much just IP protocol; decide which physical path the data will take
- Link Layer: One-hop communication: Ethernet, WiFi; Defines the format of data on the internet
- Physical Layer: mechanism for one hop communication: electrical/optical/electromagnetic wave stuff. Outside of our expertise/interest; transmit raw bit stream over the physical medium.

**Delays**

- Processing delay: devices examine packets and decide what to do; usually small, devices are designed to process packets. Can be ignored.
- Propagation delay: physical signals to travel between hops; scale * distance / speed of light; shorter distance/ better material
- Transmission delay: convert from in-memory representation to a physical signal (transmission rate); data length / device transmission rate
- Queuing delay: device cannot receive and forward packets right away. Store in queues to hold. Unpredictable and highly variable

**Traffic** **intensity**: L = average length in bytes per packet; a = packets per second; R = transmission rate; a*L = incoming rate; Traffic intensity = a*L/R; Less than 1 = receiving less = queues get shorter over time. Greater than 1 = will grow to full and drop packets

**RTT** (Round Trip Time): send a packet to another host and receive a response from it. Assume that any difference in the round-trip time (RTT) for the same sized packets to the same host, is due to queuing delays. The minimum RTT = 0 queuing delay. Propagation = physical distance.

TTL (Time to Live): number of hops it’s allowed to travel before it should be dropped.

**Traceroute**: The traceroute tool sends packets with increasing TTL values and will measure the RTT of any packet that gets a response. Not all devices send a response when dropping packets so instead of a time, traceroute prints *.

**Throughput**: the amount of data (bits/s) that can be transmitted between hosts.

**Bottleneck**: nodes are the minimum throughput devices on a path, typically located at/near connections to access networks

[Application Layer](Network%20fa41f26c3f6d419ebe6b9c441e0d4c34/Application%20Layer%20a6826b9e13944150ae9956698399f225.md)

[Transport Layer](Network%20fa41f26c3f6d419ebe6b9c441e0d4c34/Transport%20Layer%205b5146f1eaf040219229fd298302c20f.md)

[Network Layer](Network%20fa41f26c3f6d419ebe6b9c441e0d4c34/Network%20Layer%20af88cdb4b163473889a0750379619e06.md)

[Link Layer](Network%20fa41f26c3f6d419ebe6b9c441e0d4c34/Link%20Layer%20cb42e478710841d88bb8800f3b7c2d04.md)