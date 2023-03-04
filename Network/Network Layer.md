# Network Layer

The network layer sits between the link and transport layers. Routers are the main devices that make the network layer work.

At the endpoints, the communication between network/transport layer is mostly just passing packets up/down. In the middle of the network, network layer devices don't touch the transport layer.

The link layer will send packets to the “next hop” for the network layer, so the network layer's job is to determine what the “next hop” is.

**Routers:**

- receive from input links and forward to output links.
- Input link = strip off link layer stuff; Output link = add link layer info.
- Routing fabric: connects the links together so they can be passed from input to output.

**IP address:** are assigned intentionally. The more prefix bits that 2 IP addresses have in common, the closer they are physically.

**Forwarding Tables**: The entries are rules. Each rule is an IP prefix and the output link to use for packets destined to that prefix. Classless interdomain routing = buy any length of prefixes.

**DHCP (Dynamic Host Configuration Protocol):** assign IPs. Tracking which addresses are in use and responding to requests for IP address assignment.

- The client first sends a broadcast message to IP 255.255.255.255 that goes to all the devices on the same subnet.
- Subnet = a set of interfaces with the same IP prefix that are connected without going through any routers. (Wifi router or switch)
- Client broadcasts ‘DHCP discover’ – Server broadcasts ‘DHCP offer’ – client broadcasts ‘request’ asking for the address in the offer – Server broadcasts ‘ACK’ – client uses IP

**IPv4 packet:** src and des IPv4 addresses (32 bits each), packet length, fragmentation info, time to live, protocol, header checksum.

- Address shortage: 2^32 IPs and more than 4b devices.

**NAT (Network Address Translation):** use port numbers to get some extra ID bits.

- Modem operates as a NAT gateway which translates between IP/Port pairs “in front of” and “behind” the NAT.
- Pro/Con:
    - NAT basically, seamlessly enables many devices to share a public IP address.
    - Since port numbers are 16 bits, it can handle 216 simultaneous connections for NATed devices.
    - For TCP connections, it can monitor SYN/FIN bits and knows when it can remove a mapping. For UDP, it can't do that and must rely on heuristics.
    - Servers which are behind a NAT must set up “port forwarding” because by default NAT mappings are only created when NATed devices behave as clients
    - NAT routers can be a “single point of failure” or bottleneck because each connection must use the same NAT device to work properly

**IPv6:** 128-bit addresses. IPv6 eliminates the checksum and fragmentation. No business incentive.

**Generalized Routers:** Match and Action. Devices “match” packets based on some criteria (src/des IP or port, possibly other data), and an action is performed (forwarded to a particular link, NAT translated, etc). You can design other operations based on these ideas, firewalls.

**Control Plane:** the systems/algorithms that determine the forwarding tables for routers.

Software defined networking: having routers that are controlled/programmable.

**Routing algorithms:** The routers need to know which output link to forward packets to based on the IP prefix of their destination.

- Network is a weighted graph = solve the “single source shortest paths” problem
- **Dijkstra’s algorithm (link state):**
    - OSPF (Open Shortest Path First): sharing info about “link states” at a node, basically the edge cost at that node.
    - If a node listens for all these broadcasts, it knows all the edges in the graph, so can run Dijkstra’s algorithm locally and compute a forwarding table accordingly.
    - For each prefix, we just use the first link in our path to fill in the appropriate forwarding table entry.
- **Bellman Ford algorithm (Distance vector):** relies on solving a simple, obvious equation
    - Dist(x, y) = min(edge(x , n) + dist(n, y)) where we take the minimum over all n
    - For each neighbor we need to know our neighbor’s distance estimates to other n.
    - Each node broadcasts to its neighbors its distance vector. Update dv.
- The whole internet is too big to run Dijkstra.

**Autonomous systems (AS):** a network of sub networks. We can run dijkstra's/BF algorithms within an AS but use different algorithms to route between AS's. Different AS's are often run by different companies/organizations so they won’t be centrally managed.

BGP (Border gateway protocol): used for AS to coordinate/cooperate. eBGP/iBGP.

Routing with AS: hot potato = tries to get packets out of the ASs as quickly as possible, so basically route to a border router ASAP. Affected by business decisions.

**IP Anycast:** an IP address can belong to any of a number of devices. Note, this works great for DNS since there is just a one packet and response. For TCP, if packets got routed to different devices, that wouldn't work.