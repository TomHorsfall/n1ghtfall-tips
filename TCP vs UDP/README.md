# TCP vs UDP Protocols


### TCP aka Transmission Control Protocol
- Is a connection-oriented protocol (think of it like a handshake)
- Determine how to break application data into packets that networks can deliver
- Sends packets to and accepts packets from the network layer
- Manages flow control
- Handles re-transmission of dropped or garbled packets as its meant to provide error-free data trasnmission and
- acknowledges all packets that arrive. 

### Why is TCP Important?
- It establishes the rules and standard procedures for how information is communicated over the internet.
- it is the foundation of the internet as it currently exists and ensures that data transmission is carried out uniformily. 
- It is used for organizing data in a way that ensures the secure transmission between the server and client. For this reason it is used to transmit data from other higher level protocls that require all transmitted data to arrive. 


Common Protocols that use TCP:

- HTTP
- SSH
- SMTP



### UDP aka User Datagram Protocol
- Is connectionless (think of it like streaming a movie from a website or maybe like a person huckin an endless number of sticks into a woodchipper)
- Is typically used for highly time sensistive applications such as Voice over IP, streaming video and gaming
- Reduces latency (latency: the delay before a transfer of data begins follwioing an instruction for its transfer)
- Does not re-order or transmit missing data. It just continues sending new data. What makes it goes on and what doesn't gets dropped. 
- Has no way of detecting whether both applications have finished their back and forth communciation
- instead of correcting invalid data packets UDP discards those packets and defers to the Application Layer for more detailed error detection. 
