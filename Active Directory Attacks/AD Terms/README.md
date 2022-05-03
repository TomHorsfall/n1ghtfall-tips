# AD Terms to Know

1. [Authentication](#authentication):
    - [NTLM Authentication](#ntlm)
    - [Kerberos Authentication](#kerberos-authentication)
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

NTLM Hashes are not the most secure and can be easily cracked within a few days with modest equipment. 


## Kerberos Authentication

A ticket system created by Microsoft to increase security that lacked in NTLM. 

in this system the Domain Controller is used as a Key Distribution Center to access services across a network. 

Here we can quickly go through the steps of Kerberos Authentication which I am going to breakdown into 3 stages:

### A. AS_REQ Stage (Authenticate to the DC)
1. A user logs into a workstation and a **request is sent to the DC**. This is called an **Authentication Server Request (AS_REQ)**

What is in the **AS_REQ**?:
- A timestamp encrypted using the user's hashed password
- The username of the user trying to authenticate

2. When the DC receives the request it looks up the password hash associated with that user and attempts to decrypt the timestamp. If the timestamp decryption is successful AND the timestamp isn't a duplicate (aka a replay attack) the authentication is successful. 
### B. AS_REP Stage (Receive a Reply from the DC)
3. The DC replies to the client with an **Authentication Server Reply (AS_REP)** that contains
- A session key (Kerberos is stateless aka it doesn't keep track of login activity)
    - The session key is encrypted using the user's hashed password. (This is a vulnerability)
- A **Ticket Granting Ticket (TGT)**

To not get confused moving forward here are some notes about the TGT. 

Information contained in a TGT is all associated with the user that has authenticated. Including:
 a. Group memberships (permissions the user has)
 b. The domain
 c. A timestamp
 d. The IP Address of the Client
 e. The session key

To avoid tampering, the TGT is encrypted by a secret known only by the KDC and cannot be decrypted by the client (knowing this, if a user somehow got ahold of the secret used by the KDC, they could use this to create false tickets which is better known as a Golden Ticket Attack)

- The TGT is valid for 10 hours by default after which it is automatically renewed without the need for re-entering their password. 

### C. TGS_REQ Stage (Requesting access to a service on the network)
4. When a user wishes to access a service or resource on the domain (this could be a network share, a printer, an internal web application, etc.) that has a **Registered Service Principal Name** the user must contact the KDC again (located at the DC). 
- Essentially a Service Principal Name (SPN) is the name of a service a user might want to connect to. 

The user computer contacts the KDC by creating a **Ticket Granting Service Request (TGS_REQ)** packet that contains:
a. The current user
b. A timestamp encrypted using the session key
c. The SPN of the resource
d. The encrypted TGT

5. The **Ticket Granting Service** on the KDC receives the TGS_REQ and if the SPN exists in the domain, the TGT is decrypted using the secret key known only to the KDC (KRBTGT user)

Several things happen at this stage that make my head hurt. It's a lot to remember:

a. The session key is extracted from the TGT and used to decrypt the username and timestamp of the request. This allows the system to:

i. Check the timestamp and verify this is not a replay attack
ii. Verify that the username from the TGT is the same as the username from the TGS_REQ
iii. The client IP address needs to coincide with the TGT IP Address

### D. TGS_REP Stage: If all of the above is successful then you get a Ticket Granting Server Reply

If everything works up to this point the user will get a TGS_REP packet which contains:
i. The SPN to which access has been granted (Encrypted using the session key associated with the TGT)
ii. A Session key to be used between the client and the SPN (Encrypted using the session key associated with the TGT)
iii. A service ticket containing the username and group memberships along with the newly created session key. (encrypted using the password hash of the service account registered with the SPN in question) (This is a vuln aka kerberoasting)













## KDC (Key Distribution Center)






