# TCP (Transmission Control Protocol)

TCP is the most common transport layer protocol**.**

It provides a “connection oriented” interface**.** It provides reliable data transfer. It provides “flow” control and “congestion” control. It hasn't changed much in 50 years. TCP “Packets” are called “Segments”. Point to Point = 2 processes talk to each other and cannot broadcast to multiple recipients. Full duplex = both sides can send data at any time, even simultaneously.

**TCP header:**

- source and destination port numbers (process identification)
- sequence and ack numbers (for reliable data transfer)
- flags (managing state of the connection)
- receive window (flow control)

**TCP handshake:**

- 3-way handshake: make sure both sides understand the protocol and do basic setup
- Client send SYN + random sequence number; Server response SYNACK (based on client SEQ) + random SEQ; Client send another ACK + data; Connection ended with FIN flags.
- ACK is the byte number of the next byte we expect to receive.
- If everything has been received/acked, the next sequence number will have the ACK number of the last received ACK. SEQ on one side is related to ACK on the other side.

**Receive buffer:** for data received. If receive too much, buffer fills up and packets dropped.

**Receive window (rwnd):** number of bytes available in the receive buffer. Determine the other side’s window size of pipelining. = Flow Control.

**Fast retransmit:** 2 same ACKs = later packet received = gap in buffer. 3 ACKs = resend before timeout.

**Timeout:** estimates RTT with an exponentially weighted moving average.

- RTT Estimate= (1 – a) * estimate + a * latest RTT; a = 1/8
- Var Estimate = (1 - beta) * Var Estimate + beta * abs (packet RTT - estimate)
- The timeout = RTT + 4*variance

**Congestion control:** congestion window = cwnd; window size for pipelining is min(rwnd, cwnd). When packets are dropped = network congestion. 3 states:

- **Slow start:** start with a small cwnd: 1 packet = MSS = maximum segment size; each time get a new ACK cwnd += MSS (double)
- **Congestion avoidance:** when cross slow start threshold (ssthresh), cwnd + 1 MSS
    - Timeout: go back to slow start, set cwnd = 1 MSS
    - 3 duplicate ACKs: fast recovery, set cwnd = cwnd/2
    - Ssthresh = cwnd/2
- **Fast recovery:** duplicate ACK, increase cwnd slightly. New ACK, back to stage 2. Timeout, back to stage 1.

**AIMD:** additive increase, multiplicative decrease. 75% of the theoretical max. Fair = over time, multiple TCP connections will transmit at the same rate.

Head of line blocking: if we use one socket and any packet is dropped none of the received data can be passed to the app layer.

**QUIC:** UDP internet connections. Connection identifier to avoid parking lot problem. Multiple “streams” are supported with one QUIC connection, dropped packet only delay streams. Initial QUIC handshake is like TCP + TLS. Reconnecting = know client can send in the first packet.