# AD Terms to Know

Resources used to create this page:
- https://www.sciencedirect.com/topics/computer-science/ticket-granting-service 


1. [Authentication](#authentication):
    - [NTLM Authentication](#ntlm)
    - [Kerberos Authentication](#kerberos-authentication)
        - [AS_REQ](#a-asreq-stage-authenticate-to-the-dc)
        - [AS_REP](#b-asrep-stage-receive-a-reply-from-the-dc)
        - [TGS_REQ](#c-tgsreq-stage-requesting-access-to-a-service-on-the-network)
        - [TGS_REP](#d-tgsrep-stage-if-all-of-the-above-is-successful-then-you-get-a-ticket-granting-server-reply)
2. [KDC (Key Distribution Center)](#kdc-key-distribution-center)
3. [Registered Service Principal Name (SPNs)]
Understanding Cached Credentials and Storage

### Authentication

## NTLM (New Technology Lan Manager Authentication)

NTLM is a way of performing authentication against a server. There are multiple steps involved in this process. 

1. The client computer calculates a cryptographic hash of the user's password. 
2. Client sends the **username** to the server
3. Server returns a **nonce** or **challenge** that contains a random value
4. The client computer encrypts this nonce using the user's hashed password.
5. The client computer forwards this hashed nonce (the **response**) and the username back to the server.
6. The server forwards the **response** on to the domain controller since it already knows the NTLM hash of all of the users. 
7. The domain controller encrypts the **nonce** using the hashed password stored for that particular user. 
8. If the response provided by the user is the same as the **nonce/ challenge** that is hashed by the stored password in the DC, the authentication is successful. 

NTLM Hashes are not the most secure and can be easily cracked within a few days with modest equipment. NTLM is also easily exploitable using Pass-The-Hash or by taking passwords offline and cracking them (can do this using a tool called Mimikatz)


## Kerberos Authentication

- A ticket system created by Microsoft to increase security that lacked in NTLM. 
- In this system the Domain Controller is used as a Key Distribution Center to access services across a network. 


## KDC (Key Distribution Center)

Resource Used: https://www.sciencedirect.com/topics/computer-science/ticket-granting-service

The Key Distribution Center is the center of the Kerberos process. The KDC holds a database of the keys used in the authentication process and consists of two main parts: An **Authentication Service** and a **Ticket Granting Service**

### Authentication Service
    - As it very clearly says in the title, this portion of the KDC is used to authenticate the client (aka the person or user attempting to authenticate via Kerberos)

### Ticket Granting Service
    - The Ticket Granting Service is utilized after the client has authenticated and is used to provide ***tickets*** and ***Ticket Granting Tickets*** to the client systems. 

### Ticket Granting Tickets (TGTs)
    Questions to ask yourself:

    - What is in a TGT?
        1. The client ID (aka the username of the user trying to authenticate)
        2. The client IP Address (The machine on the network that is authenticating)
        3. The ticket validity period (aka a timestamp. These tickets last 10 hours.)
        4. The ***Ticket Granting Server Session Key***

Here we can quickly go through the steps of Kerberos Authentication which I am going to breakdown into 3 stages:

## Kerberos Authentication Explained (Steps A through E):

### A. AS_REQ Stage (Authenticate to the DC)
1. A user logs into a workstation and a **request is sent to the DC**. This is called an **Authentication Server Request (AS_REQ)**

What is in the **AS_REQ**?:
- A timestamp encrypted using the user's hashed password
- The username of the user trying to authenticate

2. When the DC receives the request it looks up the password hash associated with that user and attempts to decrypt the timestamp. If the timestamp decryption is successful AND the timestamp isn't a duplicate (aka a replay attack) the authentication is successful. 
### B. AS_REP Stage (Receive a Reply from the DC)
3. The DC replies to the client with an **Authentication Server Reply (AS_REP)** that contains
- A session key (Kerberos is stateless aka it doesn't keep track of login activity)
    - The session key is encrypted using the user's hashed password.
        - It may be decrypted by the client and re-used
- A **Ticket Granting Ticket (TGT)**

To not get confused moving forward here are some notes about the TGT. 

Information contained in a TGT is all associated with the user that has authenticated. Including:
- Group memberships (permissions the user has)
- The domain
- A timestamp
- The IP Address of the Client
- The session key

To avoid tampering, the TGT is encrypted by a secret known only by the KDC and cannot be decrypted by the client (knowing this, if a user somehow got ahold of the secret used by the KDC, they could use this to create false tickets which is better known as a Golden Ticket Attack)

- The TGT is valid for 10 hours by default after which it is automatically renewed without the need for re-entering their password. 

### C. TGS_REQ Stage (Requesting access to a service on the network)
4. When a user wishes to access a service or resource on the domain (this could be a network share, a printer, an internal web application, etc.) that has a **Registered Service Principal Name** the user must contact the KDC again (located at the DC). 
- Essentially a Service Principal Name (SPN) is the name of a service a user might want to connect to. 

    The user computer contacts the KDC by creating a **Ticket Granting Service Request (TGS_REQ)** packet that contains:
    1. The current user
    2. A timestamp encrypted using the session key
    3. The SPN of the resource
    4. The encrypted TGT

5. The **Ticket Granting Service** on the KDC receives the TGS_REQ and if the SPN exists in the domain (This can be exploited if an attacker gains access to a machine, pre-auth is turned off, and the attacker brute forces for common SPNs), the TGT is decrypted using the secret key known only to the KDC (KRBTGT user)

Several things happen at this stage that make my head hurt. It's a lot to remember:

- The session key is extracted from the TGT and used to decrypt the username and timestamp of the request. This allows the system to:
    - Check the timestamp and verify this is not a replay attack
    - Verify that the username from the TGT is the same as the username from the TGS_REQ
    - The client IP address needs to coincide with the TGT IP Address

### D. TGS_REP Stage: If all of the above is successful then you get a Ticket Granting Server Reply

6. If everything works up to this point the user will get a TGS_REP packet which contains:
- The SPN to which access has been granted (Encrypted using the session key associated with the TGT)
- A Session key to be used between the client and the SPN (Encrypted using the session key associated with the TGT)
-  A service ticket containing the username and group memberships along with the newly created session key. (encrypted using the password hash of the service account registered with the SPN in question) (This is a vuln aka kerberoasting because if the attacker brute forced for SPNs and they now have access to the service account hash, they can take it offline and try to crack it.)

Once the authentication process by the KDC is complete and the client has both a session key and a service ticket, the service authentication begins.

### E. AP_REQ: After all that crap NOW the user can try to authenticate to the Application server (AKA what service it wants to access)
7. The client sends to the Application server an ***application request*** or AP_REQ which includes:
- The encrypted username and timestamp (using the session key associated with the service ticket)
- The service ticket itself

8. The application server decrypts the service ticket using the service account password hash and extracts the username and the session key. 
- It then uses the session key to decrypt the username from the AP_REQ .
    - If the AP_REQ username matches the one decrypted from the service ticket the request is accepted. 
    - Before access is granted the service inspects the supplied group memerships in the service ticket and assigns the appropriate permissions to the user
        - After this, the user may access the requested service 








