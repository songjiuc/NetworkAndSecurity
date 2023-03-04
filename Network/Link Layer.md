# Link Layer

The link layer is responsible for “next hop” communication. It takes “network layer packets” and “frames them” to create “link layer frames”

- “point to point” protocols like ethernet are for when there is no interference. These link layer protocols are simple.
- “broadcast” protocols are like WIFI where many devices share the same physical layer channel and can interfere. Dealing with interference is a difficult and interesting problem.

**Error detection:** checksum and correction (potentially resending). Transport layer detection = faster + easier.

**Parity checking:** xor all the bits together and append one extra bit. If 1 is odd, add 1, if 1 is even, add 0 = always even. If odd number of flips, it detects 1.

**Broadcast Channels:** many devices use the same physical channel for sending data. All devices can receive all messages sent over the channel.

- If only 1 device is transmitting, it should use all available bandwidth and send fast.
- If multiple devices are transmitting, resources should be distributed fairly.

**Slotted ALOHA:** all devices have a synchronized clock, divided into slots – send N bytes. When a device has data to send, it tries to send it in the next time slot. Multiple device = collisions = resend.

- Random Backoff: flip a coin to decide whether to resend in the next time slot or to wait another time slot. Sometimes only 1 device will retry. 37% slots are used.

**Unslotted ALOHA:** each device’s time slots will be out of sync with each other. Half of 37%.

**CSMA (Carrier-sense multiple access):** add common sense to unslotted aloha. Listen to see if another node is transmitting and wait until they stop before we start sending.

- Binary exponential backoff: choose a random number of timeslots to wait between 1 and 2^number of collisions for the packet.
- The faster collisions are detected, the better CSMA performs.

**Taking turns:** a device is assigned a timeslot every numNodes slots. Fair but waste. Who decides when. Or that node crashes.

Data Over Cable Service Interface Specification (DOCSIS): cable internetis a broadcast channel. Cable modem termination system (CMTS) has a shared link to you and neighbors.

- Downloading: ISP is broadcasting to all neighbors and modem drops all packets.
- Uploading: clients request upload time for several slots. Pick slots randomly and hope for no collisions. CMTS assigns slot based on the request and announces. Slot assigned = upload; not assigned = wait for next upload request round.

**LAN (Local Area Networks)**

**Switches:** like a router but operates at the link layer. Switches operate transparently to hosts, and basically hosts can't tell that they're there. Switches are also self-configuring so you don't need to provide them with a forwarding table... they start working as soon as they're plugged in!

- Forward packets based on the dest MAC
- Automatically fill in a forwarding table by examine packets sent through them.
- Address yes = know direction; no = broadcast to all links except the one it came from, and then fill in an entry when the host responds.

**MAC (Media Access Control) address**: not assigned for user convenience. Allocated to device manufactures.

**ARP (Address Resolution Protocol):** like DNS and answer queries: what is MAC for the IP? Broadcast MAC address all 1s. ARP message has the sender MAC address in the header so the device can respond directly to the device with an ARP response. ARP table = IP->MAC.

Ethernet

**Frame:** src/dest MAC address; checksum (CRC: Cyclic Redundancy Check algorithm); network layer type (in theory it works with non-IP network layers); preamble : this is for synchronizing transmission rate at the physical layer level.

**Switches vs Hubs vs Routers**

- Switches and hubs operate at the link layer and route packets based on MAC address. They don't need to look at the network layer headers at all.
- Hubs broadcast all packets out all links (except the one the packet came from), they don't have a switching table which learns which MAC addresses are on which output links.
- Switches/Hubs are zero-configuration, you plug them in, and they start working. Routers need explicit setup to set up forwarding tables.
- Switches/Hubs are “transparent” to network devices. Routers have IP addresses and are an explicit part of network layer operation.

Switches require no configuration, which is nice, but multiple switches can only be configured in a tree topology. Switches can't do hierarchical routing since MAC addresses aren't “organized” in any useful way. Typically a big network will be designed using a combination of routers and switches.

**VLANs (virtual LAN):** A switch can virtually separate its links into separate LANs by keeping separate ARP tables for the separate subnets.

Usually those devices can also act as network layer routers and so can route packets between the VLANs at the network layer

“Trunk Ports” are links that are considered to be part of all vLANs so different physical switches can be used to “host” the same vLAN