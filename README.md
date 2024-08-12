# HTTPS                      
* HTTPS (Hypertext Transfer Protocol Secure) is used to secure communication over the internet. It ensures that data exchanged between a user's web browser and a web server is (server - client) encrpted.
* HTTPS verifies the identity of the website through TLS certificates, ensuring that the user is communicating with the intended website and not a malicious actor.
* HTTPS ensures that the data transmitted has not been altered in transit. Any modification of the data will be detected, protecting against tampering.
  
### TLS Certificate                
* TLS/SSL certificates are unique to the server or the domain it is issued for.
* A TLS certificate is provided by organizations known as Certificate Athorities (CAs). These are trusted entries responsible for issuing and managing digital certificates. Here are some of the most well-known Certificate Authorities - Let's Encrpt, DigiCert, GlobalSign, Comodo, GoDaddy etc..
* During the TLS handshake process the server sends the TLS certificate which is then verified by then client.
* **What Does the Client Verify the Certificate Against?**
  * Trust Store: The client verifies the certificate against the list of trusted root certificates in its trust store.
  * Domain Name: The certificate is verified against the domain name the client is trying to connect to.
  * Revocation Status: The client checks against CRLs or uses OCSP to verify that the certificate has not been revoked.
  * Cryptographic Integrity: The client verifies the digital signature using the public key of the issuing CA.

### Cipher Suites          
* In the whole TLS session different algorithms are used for data encrption and other process.
* The cipher suite specifies the algorithm used in each process. The algorithms specified in the cipher suite are -
  * Key Exchange Algorithm - Determines how the initial ecrption keys will be exchanged between client and server.
  * Athentication Algorithm - Ensure that the identity of the communicating parties (client and server) is verified.
  * Symmetric Encrption Algorithm - Encrpts the data transmitted between the client and server once the initial exchange has been completed.
  * Message Authenticatin Code (MAC) Algorithm - Provides the data intergrity and ensures that the transmitted data has not been tampered with.
* During the TLS handshake process, the client and server negotiate and agree upon a cipher suite to use for the session.
  * Client Hello : The client sends a list of supported cipher suites to the server.
  * Server Hello : The server selects a cipher suite from the list and informs the client of its choice.

![image](https://github.com/user-attachments/assets/0a02c6b0-fef4-4b2a-9642-289e68e5d105)

### TLS Handshake Process      
![image](https://github.com/user-attachments/assets/40e26a44-13d1-48b6-bbc6-605775ef351d)
           
1. Client Hello
   * A list of supported TLS versions.
   * A list of supported cipher suites.
   * A randomly generated number (client random).
   * Any other extentions, such as the Server Name Indication (SNI).
2. Server Hello
  * The choosen TLS version.
  * The choosen cipher suite.
  * A randomly generated number (server random).
3. Certificate
  * The server's digital certificate, containing the server's public key.
4. Sever Key Exchange
  * The server may send a "Server Key Exchange" message if the selected cipher suite requires it.
5. Server Hello Done
  *  The server indicates it has finished its part of the handshake by sending a "Server Hello Done" message.
6. Key Generation
  * Both the client and server genrate the session keys.
  *  Master Secret: Both the client and server use the pre-master secret (from RSA) or the shared secret (from DH/ECDHE), along with the client random and server random, to generate a "master secret."
  * Session Keys: The master secret is then used to derive the following session keys:
    * Client MAC Key: For ensuring data integrity of messages sent by the client.
    * Server MAC Key: For ensuring data integrity of messages sent by the server.
    * Client Encryption Key: For encrypting data sent by the client.
    * Server Encryption Key: For encrypting data sent by the server.
    * Initialization Vectors (IVs): Used in certain encryption modes (e.g., CBC) to randomize encryption.
7. Client Finished
  * The client sends a "Finished" message, which is the first message encrypted with the session keys.
8. Server Finished
  * The server responds with a "Finished" message, indicating that the handshake is complete.
9. Secure Communication Begins
  * After the handshake, both the client and server start exchanging application data, such as HTTP requests and responses.
  * Client Encryption Key: Used to encrypt data sent by the client.
  * Server Encryption Key: Used to encrypt data sent by the server.
  * Client and Server MAC Keys: Used to verify the integrity of each data packet sent during the session.


