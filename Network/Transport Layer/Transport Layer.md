# Transport Layer

**Transport Layer**

Transport layer is responsible for “process to process” communication, which means it needs a way to identify individual processes on hosts, port number. Ports below 1024 are privileged.

Clients need a port number, which is assigned by the OS arbitrarily. Ephemeral. 80 = HTTP; 443 = HTTPS; 53 = DNS. TCP has a connection, UDP doesn’t.

**RDT** (Reliable Data Transfer): Network is unreliable. Both TCP/UDP provides error checking for packet corruption, but TCP also handles packets that are dropped or arrive out of order. TCP guarantees that any data being sent to the app layer is the data the sender intended, in the order that they sent it. It can’t guarantee that the data gets there.

**Transport** **layer** **interfaces**: App layer = deliverToApp(bytes) + sendData(bytes); Network layer = sendPacket(bytes) + receivePacket(bytes)

**Bit** **errors**: assume packets are corrupted but not dropped. We need: error detection, receiver feedback, and retransmission. Detects an error = retransmission, otherwise acknowledge.

**FSM** (Finite State Machines): In an FSM, the system is in a finite set of “states” and transitions between them when actions occur.

Checksum, acknowledgement (ACK/NACK), timeout, sequence number, pipelining (to not wait for at least an RTT, be faster).

**Go** **back** **N**: packets can be in 3 states: sent ACKed, sent not ACKed, unsent. The send has a window of un-ACKed packets in flight (N packets). When packets are ACKed, the window slides forward. The receiver ACKs the number of the highest in-order packet it has received.

**Selective** **Repeat**: Any packet in the “sliding window” can be ACKed as it’s received. The ACKs aren’t cumulative. The sender must receive an ACK for every single packet to be sure that it was received. Compared with GBN, SR requires more ACKs to be sent, but can prevent the sender from resending a bunch of packets if the first in a burst is lost.

[TCP (Transmission Control Protocol)](Transport%20Layer%205b5146f1eaf040219229fd298302c20f/TCP%20(Transmission%20Control%20Protocol)%20880321fa889b485fa29ec8c74763da0a.md)