<!-- vscode-markdown-toc -->
- [Protocols](#protocols)
- [Brief](#brief)
  - [SSL](#ssl)
  - [XMPP](#xmpp)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
  
## <a name='Protocols'></a>Protocols

Protocols are set of rules or standards that define how data is transmitted or received between devices on network. It ensures that devices can communicate with each other in a consistent and understood manner. Think of it as a common language that devices use to talk to each other.
Types of protocols:
- `Communication Protocols`: Communication protocols are rules that allow devices to exchange data. They can be categorized based on their function, such as messaging, ral-time communcation, email, file transfer etc.
  a. `Messaging & Presence Protocols`:
    -   SIP
    -   [💉](#XMPP)XMPP
    -   MQTT
    -   AMQP
- `Networking Protocols`: Networking Protocols are the rules and standards that govern data communication between devices in a network, ensuring accurant transmission.
  - `HTTP`: HyperText Transfer Protocol, where all the information is sent in clearText.
  - `HTTPS`: HyperText Transfer Protocol Secure, a secured verison of HTTP. HTTPS encrypts the data that is retrieved by using encryption algorithm to scramble the data being transferred. HTTPS secure the data using one of two protocols:
    - `SSL`: Secure Sockets Layer is a protocol used to ensure data security on the internet by use of public-key encryption.
  - `FTP`:
  - `TCP/IP`: 
- `Routine Protocols`
- `Security Protocols`
- `Data Link Layer Protocols`
- `Application Layer Protocols`
- `IoT Protocols`

## <a name='Brief'></a>Brief

### <a name='SSL'></a>SSL
SSL or Secure Sockets Layer, is an encryption-based Internet security protocol, developed by Netscape in 1995 for the purpose of ensuring privacy, authentication and data intergrity in Internet communications. SSL is predecssor of modern `TLS` encryption used today.<br>
A website that implements SSL/TLS has *HTTPS* in it's url instead of *HTTP*.
- `Process involved in SSL/TLS encyption`:
  - *Encrypts data* that is transmitted across web.
  - *Initiates an authentication process* called Handshake between two communicating devices.
  - Digitally signs in order to provide *data inegrity*, verifying that data is not tampered before reaching.
- SSL has not been updated since SSL 3.0 in 1996 and is now deprecated. TLS is the up-to-date encryption protocol that is being used nowadays but people still tag it as SSL only.
- `SSL Certificate`: SSL can only be implemented by websites that have an SSL certificate. It's like a card that proves someone is who they say they are. It's stored and displayed on the Web by a website's or application's server. One of the most important piecies of info in an SSL certificate is website's public key, which makes the encryption and authentication possible. User's device uses the public key to estblish secure encryption keys with web server. And web server stores a private key, that decrypts data encrpted with the public key.
- `Types of SSL certificates`:
  - Single-domain: Applies to only one domain.
  - Wildcard: Applies to only one domain but also includes subdomains. Like www.cloudfare.com, blog.cloudfare.com.
  - Multi-domain: Can apply to mulitple unrelated domains.
- TLS uses `public key cryptography`, in which there are two keys, a public key shared with client via server''s SSL certificate and a private key. When client opens a connectionwith server the two devices uses the both keys to agree on a new key called `session key`, to encrypt further communcations between them. All HTTP requests and responses are then encrypted with these session keys.

### <a name='XMPP'></a>XMPP
XMPP stands for Extensible Messaging and Presence Protocol, a communcation protocol used for instant messaging, presence information, and online collcaboration.XMPP messages are encoded in XML. 
- Key features:
  - `Decentralized archiecture`: It's decentralized, meaning anyone can setup an XMPP server, unlike centralized services like WhatsApp or Facebook Messenger.
  - `Real-time Communication`: Supports real-time message delivery.
  - `Extensible`: Due to XML based design, XMPP can be extended with new features, allowing developers to create custom functionalities.
  - `Security`: XMPP supports encryption protocols such as TLS and SASL for secure communications.
- WhatsApp initially used XMPP as its core messaging protocol. However, it has since customized the protocol significantly to suit its infrastructure, adding encryption and various optiomizations. It also uses **Signal Protocol** for end-to-end encryption.
- Drawbacks (why WhatsApp evolved over XMPP):
  - `Scalability Issues`:
    - XMPP is designed as decentralized protocol, while this is beneficial for small-scale, it can be challenging to optimize and control in a large-scale, ccentralized systems like WhatsApp or Messenger.
    - XMPP requires persistent TCP connections, which can strain servers when dealing with millions or billions of concurrent users.
  - `Message Delivery Optimizations`: 
    - XMPP wasn't designed to handle seamless message synchronization across multiple devices.
    - Although XMPP can handle offline messaging, optimizing this for millions of users who may come online and offline frequently is difficult at scale.
  - `Media and File Transfers`:
    - XMPP can handle basic file transfers but doesn't have built-in mechanism to optimize image, video or voice message compression and transfer.
    - XMPP focus is primarily on text-based communications, and it would require significant customization to achiece the real-time performance necessary for large-scale audio/video calls.
  - `Security & Encryption`: 
    - XMPP supports mechanism for transport-level encryption (eg using TLS) but not end-to-end encryption by default.
    - Doesn't supports large platform's specific security requirements like message self-destruction, disapperaing messages etc.
  - `Horizontal Scalability and Load Balancing`: 
    -  XMPP wasn't designed with modern cloud-native horizontal scalability in mind. Large platforms often need to scale horizontally across thousands of servers. Although clustering solutions exist for XMPP, they require significant effort to implement efficiently, and many companies prefer to develop custom solutions optimized for their infrastructure.
  