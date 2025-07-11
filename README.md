# microTCP Implementation

A lightweight TCP-like protocol implementation for educational purposes, providing reliable data transmission over UDP.

## Features

- **Connection Management**:
  - Three-way handshake (SYN, SYN-ACK, ACK)
  - Graceful connection termination (FIN, ACK)
  
- **Reliable Data Transfer**:
  - Sequence numbers and acknowledgments
  - Checksum verification
  - Retransmission on packet loss
  - Duplicate ACK detection

- **Flow Control**:
  - Sliding window mechanism
  - Dynamic window size adjustment

- **Congestion Control**:
  - Slow start phase
  - Congestion avoidance phase
  - Fast retransmit on duplicate ACKs

## Prerequisites

- Linux/Unix system
- C compiler (gcc recommended)
- Basic networking libraries (installed by default on most systems)

## The library provides the following API functions:
```c
microtcp_sock_t microtcp_socket(int domain, int type, int protocol);
int microtcp_bind(microtcp_sock_t *socket, const struct sockaddr *address, socklen_t address_len);
int microtcp_connect(microtcp_sock_t *socket, const struct sockaddr *address, socklen_t address_len);
int microtcp_accept(microtcp_sock_t *socket, struct sockaddr *address, socklen_t address_len);
int microtcp_shutdown(microtcp_sock_t *socket, int how);
ssize_t microtcp_send(microtcp_sock_t *socket, const void *buffer, size_t length, int flags);
ssize_t microtcp_recv(microtcp_sock_t *socket, void *buffer, size_t length, int flags);
```
## Implementation Notes

### State Management:
- Tracks connection state (UNKNOWN, BOUND, LISTEN, ESTABLISHED, etc.)  
- Handles state transitions during connection setup/teardown  

### Error Handling:
- Comprehensive error checking  
- Detailed error messages via `perror()`  
- State reset on critical errors  

### Performance Tracking:
- Counts packets/bytes sent/received/lost  
- Measures transmission time  

---

## Limitations

- Currently uses UDP as the underlying transport  
- Limited to single-client connections in this implementation  
- Basic congestion control without advanced algorithms like TCP Cubic  

