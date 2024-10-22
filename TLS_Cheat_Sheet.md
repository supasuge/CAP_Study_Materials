# TLS Security
- [TLS Security](#tls-security)
  - [Key Concepts in TLS](#key-concepts-in-tls)
    - [**Defining TLS Security**](#defining-tls-security)
    - [**TLS 1.0 and 1.1**](#tls-10-and-11)
    - [**TLS 1.2**](#tls-12)
    - [**TLS 1.3**](#tls-13)
    - [TLS Versions Comparisons](#tls-versions-comparisons)
      - [TLS/SSL Versions Comparison Table](#tlsssl-versions-comparison-table)
    - [Summary](#summary)
  - [TLS Version Details](#tls-version-details)
      - [SSL 2.0](#ssl-20)
      - [SSL 3.0](#ssl-30)
      - [TLS 1.0](#tls-10)
      - [TLS 1.1](#tls-11)
      - [TLS 1.2](#tls-12-1)
      - [TLS 1.3](#tls-13-1)
    - [Types of TLS Certificate Misconfigurations](#types-of-tls-certificate-misconfigurations)
    - [Examples of TLS Certificate Misconfiguration](#examples-of-tls-certificate-misconfiguration)
      - [Non-technical tools](#non-technical-tools)
      - [Recommended Configurations](#recommended-configurations)




## Key Concepts in TLS 
- **Asymmetric Encryption**: TLS uses asymmetric encryption, where two different keys (public and private) are used for encryption and decryption. 
- **Perfect Forward Secrecy (PFS)**: TLS 1.3 guarantees that session keys are unique, preventing past communications from being decrypted if a private key is compromised. 
- **Handshake Process**: TLS establishes a secure connection via a handshake process. TLS 1.3 simplifies this process, making it faster and more secure. 
- **Cipher Suites**: TLS versions determine which encryption algorithms (cipher suites) are used. TLS 1.3 limits cipher suites to only the most secure algorithms, unlike older versions.
### **Defining TLS Security**

TLS security, or Transport Layer Security, is a cryptographic protocol designed to provide secure communication between two parties, typically a client and a server. TLS is used to secure communication between a user's browser and a web server, and also to secure other types of communication such as email, file transfers, and virtual private networks (VPNs).

TLS security is composed of two main types, **TLS 1.2** and **TLS 1.3**. **TLS 1.2** is the most widely used version, and is the default for most web browsers, but **TLS 1.3** is gradually becoming more popular as it is more secure.

### **TLS 1.0 and 1.1**

**TLS 1.0** and **1.1** were the first versions of TLS security, and were released in 1999 and 2006, respectively. While **TLS 1.0** and **1.1** can still be used to secure communication between two parties, they are considered less secure than **TLS 1.2** and **1.3**.

**TLS 1.0** and **1.1** use symmetric encryption to secure the connection, meaning that the same key is used to encrypt and decrypt the data. This makes them vulnerable to certain attacks, such as man-in-the-middle attacks, where the attacker can intercept the communication and access the data. Additionally, **TLS 1.0** and **1.1** do not support modern authentication protocols such as Elliptic Curve Cryptography, making them vulnerable to remote code execution attacks.

For these reasons, it is strongly recommended to use **TLS 1.2** or **TLS 1.3** for secure communication, as they are more secure and support modern authentication protocols.

### **TLS 1.2**


**TLS 1.2** is the most widely used version of TLS security. It was first released in 2008, and is used to secure communication between two parties using a combination of encryption, authentication, and data integrity.

**TLS 1.2** uses symmetric encryption to secure the connection, meaning that the same key is used to encrypt and decrypt the data. It also uses authentication to ensure that the two parties involved in the communication are who they say they are, and data integrity to ensure that the data has not been modified in transit.

An example of **TLS 1.2** in action would be a user's web browser connecting to a secure website. The browser will use **TLS 1.2** to encrypt the connection, verify the identity of the website, and ensure that the data has not been modified in transit.

### **TLS 1.3**

**TLS 1.3** is the newest version of TLS security, and is gradually becoming more popular as it is more secure than **TLS 1.2**. It was first released in 2018, and is used to secure communication between two parties using a combination of encryption, authentication, and data integrity.

**TLS 1.3** uses asymmetric encryption to secure the connection, meaning that two different keys are used to encrypt and decrypt the data. It also uses authentication to ensure that the two parties involved in the communication are who they say they are, and data integrity to ensure that the data has not been modified in transit.

An example of **TLS 1.3** in action would be a user's web browser connecting to a secure website. The browser will use **TLS 1.3** to encrypt the connection, verify the identity of the website, and ensure that the data has not been modified in transit. Additionally, **TLS 1.3** is more secure than **TLS 1.2**, as it uses a combination of encryption, authentication, and data integrity to protect the connection.

### TLS Versions Comparisons
Here's an Obsidian Markdown formatted note that summarizes the key differences between TLS versions and recommendations for usage:

Transport Layer Security (TLS) is the protocol that ensures secure communication over networks. Over the years, various versions of TLS have been released, each improving upon the previous one in terms of security and performance. This note provides a comparison between different versions of TLS and recommendations on which to use or avoid.

Here's a TLS/SSL comparison table that includes SSL versions, older TLS versions, and relevant security information, formatted for easy reference:

#### TLS/SSL Versions Comparison Table

| **TLS/SSL Version** | **Release Year** | **Key Improvements**                              | **Status**              | **Security**                            | **Should You Use It?**                                      |
| ------------------- | ---------------- | ------------------------------------------------- | ----------------------- | --------------------------------------- | ----------------------------------------------------------- |
| **SSL 2.0**         | 1995             | Original SSL protocol                             | Deprecated              | Vulnerable to multiple attacks          | **No** — Vulnerable and insecure; should not be used         |
| **SSL 3.0**         | 1996             | Enhanced security over SSL 2.0                    | Deprecated              | Vulnerable to POODLE attack             | **No** — Deprecated due to critical vulnerabilities          |
| **TLS 1.0**         | 1999             | Improved encryption algorithms based on SSL       | Deprecated (as of 2020) | Weak encryption, vulnerable to attacks  | **No** — Considered insecure and officially deprecated       |
| **TLS 1.1**         | 2006             | Added support for stronger ciphers and algorithms | Deprecated (as of 2020) | Improved but still vulnerable           | **No** — Deprecated and should not be used                   |
| **TLS 1.2**         | 2008             | Stronger encryption, modern cipher suites         | Recommended (but aging) | Secure with patches, widely used        | **Yes** — Use if TLS 1.3 is not available                    |
| **TLS 1.3**         | 2018             | Simplified handshake, improved speed and security | Highly Recommended      | Most secure version, resistant to attacks | **Yes** — Preferred for modern systems; offers the best security and performance |

---

### Summary

- SSL versions (2.0 & 3.0) are outdated and insecure. They should not be used due to serious vulnerabilities like POODLE.
- TLS 1.0 & 1.1 are deprecated and also considered insecure, so they should not be used in any modern system.
- TLS 1.2 remains secure with modern encryption but is being phased out in favor of TLS 1.3, which offers significant security and performance improvements.
  
**Recommendation**: Use TLS 1.3 for all new systems and only fall back to **TLS 1.2** if necessary for compatibility with older systems.
## TLS Version Details

#### SSL 2.0
- **Released**: 1995
- **Status**: Deprecated due to significant security vulnerabilities.
- **Key Issues**: Weak encryption and flawed handshake process make it vulnerable to Man-in-the-Middle (MitM) attacks.

#### SSL 3.0
- **Released**: 1996
- **Status**: Deprecated (vulnerable to POODLE attack).
- **Key Issues**: Although an improvement over SSL 2.0, it still suffers from significant vulnerabilities, especially to padding oracle attacks.

#### TLS 1.0
- **Released**: 1999
- **Status**: Deprecated as of 2020.
- **Key Improvements**: Introduced better encryption algorithms compared to SSL, but lacks modern security measures.
- **Why Avoid It?**: Weak encryption and vulnerable to BEAST and other modern attacks.

#### TLS 1.1
- **Released**: 2006
- **Status**: Deprecated as of 2020.
- **Key Improvements**: Enhanced encryption and protection against BEAST attacks.
- **Why Avoid It?**: Still lacks modern encryption techniques and is considered insecure by modern standards.

#### TLS 1.2
- **Released**: 2008
- **Status**: Still in use but being replaced by TLS 1.3.
- **Key Improvements**: 
  - Support for SHA-256, AES, and GCM encryption.
  - Introduction of Perfect Forward Secrecy (PFS) through ephemeral Diffie-Hellman (DHE) and Elliptic Curve Diffie-Hellman (ECDHE).
  - Provides stronger security, but it still uses a complex handshake that can lead to performance bottlenecks.
- **When to Use**: If TLS 1.3 is not available or legacy systems require it.
Vulnerable to downgrade attacks if not configured properly

#### TLS 1.3
- **Released**: 2018
- **Status**: Highly recommended and the latest version.
- **Key Improvements**:
  - Simplified handshake, reducing the number of round trips for faster connections.
  - Eliminated weaker ciphers and obsolete algorithms 
  - Perfect Forward Secrecy
  - Zero round-trip time (0-RTT) for resumption

### Types of TLS Certificate Misconfigurations
- **Certificate Expiration**: If a TLS certificate is not renewed in a timely manner, it can cause the certificate to become invalid. This can lead to a security issue, as malicious users may be able to gain access to sensitive information.
- **Improperly Configured Certificates**: If a certificate is not set up properly, it can lead to a variety of security issues. For example, a certificate may be missing a required field, or the domain may not match the certificate.
- **Using an Unsecure Certificate Authority**: If an unsecure Certificate Authority (CA) is used, it can lead to a security issue. For example, a malicious CA may be able to issue certificates with incorrect information, or the CA may not have the necessary security protocols in place.

### Examples of TLS Certificate Misconfiguration
- **Using an Outdated TLS Version**: Many web servers still use **TLS 1.0**, which is an outdated version of the protocol. This can lead to a security issue, as **TLS 1.0** is vulnerable to a variety of security attacks.
- **Incorrectly Configured Certificate Chain**: When setting up a TLS certificate chain, it is important to ensure that all certificates are properly configured. If the chain is not configured correctly, it can lead to a security issue, as malicious users may be able to gain access to sensitive information.
- **Using Weak Algorithms for Signature Verification**: If weak algorithms are used for signature verification, it can lead to a security issue. For example, a weak algorithm may be vulnerable to man-in-the-middle (MITM) attacks, data theft, and spoofing.

#### Non-technical tools
https://www.ssllabs.com/ssltest/ - Fill in your domain name, click submit, then get a A-F score for how well your SSL is configured.

#### Recommended Configurations
At [https://wiki.mozilla.org/Security/Server_Side_TLS](https://wiki.mozilla.org/Security/Server_Side_TLS), Mozilla has a few recommended configurations.
