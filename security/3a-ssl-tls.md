# Security

## 3a. SSL/TLS
[LinkedIn Course SSL Certificates for Web Developers](https://www.linkedin.com/learning/ssl-certificates-for-web-developers/why-ssl-certificates-are-essential-for-every-website?u=2162610)

### SSL Certificate
SSL certs indicate https is used fo secure communication.

A certificate certifies the ownership of a public key, and the key is used for encrypting date 
sent between a browser and a remote server.

SSL: secure socket layer, a crytographic protocol for communication security.

TLS: transport layer security.

Certificates are not dependent on the protocol.

#### Certificate Contents
* Organization
* URL
* State, country
* Valid date range
* Issuer

#### Certificate Purpose
* Encryption
* Identity
* Trustworthiness

Symmetric-key Cryptography
* encrypt data using a password
* Decrypt data using the same password
* Symmetric key == same key

Public Key Cryptography (Asymmetric-key cryptography)
* Pair of mathematically linked numbers: public key and private key
* Data encrypted with the public key, and can only be decrypted wit the private key.

SSL/TLS Hand Shake
1. A browser sends a request to a secure server.
2. The server sends back its SSL certificate, which includes the public key and the other data about
the server's identify.
3. The browser confirms the SSL certificate is valid.
4. The browser encrypts a very long password using the public key and sends it back to the server.
5. The server decrypts the data using its private key and retrieves the password.
6. They use the shared password to encrypt all future communications with symmetric-key cryptography.

Public key vs. Private key
* Public key cryptography:
  * private communication in public
  * slow algorithms
  
* Symmetric-key cryptography:
  * difficult to send key publicly
  * fast algorithms

Summary:
* SSL certificate certifies ownership of public key.
* Public key is used to exchange a password in public.
* Password used to encrypt all data between browser and server.
* Password are temporary and not reused.

#### Certificate Authorities (CAs)
* Entities that issue digital certificates.
* CAs certify the ownership of a public key.
* Provide information, an public key, and sometimes a fee.
* Get back a certificate.
* Similar to notarizing an identity.

Browsers keep a list of the CAs (their own or from the OS), the browsers trust the CAs, and a CA
has certified that a particular URL owns a public key.

Validation Levels
* Domain validation
* Organization validation
* Extended validation


#### SSL Certificate Generation
Traditional Installation
1. Generate a public-private key pair.
2. Create a certificate signing request (CSR).
3. Visit website of a CA.
4. Submit information and CSR data.
5. Wait for validation.
6. Receive certificate.
7. Manually install certificate on web server.

ACME Installation
1. Login to server.
2. Download Cerbot or other ACME client software.
3. Run software.



 




