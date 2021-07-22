# OSI
## Introduction
Theorized model, nice for learning but [TCP/IP](#TCP/IP) is the one that is actually widely used.

| Layer        | Examples       |
| ------------ | -------------- |
| Application  | HTTP, FTP      |
| Presentation | SSL, TLS       |
| Session      | NetBIOS, PPTP  |
| Transport    | TCP, UDP       |
| Network      | IP, ARP, IPSec |
| Data Link    | Ethernet, PPP  |
| Physical     | Ethernet, USB  |

## Layers
### Layer 7: Application
Interface for Softwares.
Add a header to the data.

### Layer 6: Presentation
Standardize format + transform the data (handle encryption, compression, ...).
Add a header to the data.

### Layer 5: Session
Establish a unique connection (with identifier) + track communications.
Add a header to the data.

### Layer 4: Transport
Choose protocol to transmit the data. Main ones are TCP and UDP.
TCP: Ack all packets + split message in "segments"
UDP: Send packets without caring to know if they were received + split message in "datagrams".

Add a header to the data (segments/datagrams/...)

### Layer 3: Network
Figure out the path that will be used to send the message to the destination

Add a header to the data (packets)

### Layer 2: Data Link
Add the physical address of the receiver. Also validates there is no corruption during the transmission.

Add a header + trailer to the data (frames)
This is done in order to avoid (hopefully) tampering the data.

### Layer 1: Physical
Electrical pulses, ...
Transform bits to physical signals.

# TCP/IP
## Introduction
| Layer             | OSI layers                              |
| ----------------- | --------------------------------------- |
| Application       | Application, Presentation, Session      |
| Transport         | Transport                               |
| Internet          | Network                                 |
| Network Interface | Data Link, Physical                     |

Network Interface layer may be split in 2, to reflect the OSI model.

## Open a connexion (3 way handshake)
Client                                   Server
   |   ---- SYN (Notice Me Senpai) ---->   |
   |   <------ SYN/ACK (Go ahead) ------   |
   |   -- ACK (Thank you I'll start) -->   |
