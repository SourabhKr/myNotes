# What is SSH?

The Secure Shell(SSH) is a network protocol that has been designed as a secure replacement of Telnet and others. It
allows
two connected devices to communicate securely over unsecure network. It provides encryption and authentication
mechanisms to protest data during transmission. SSH uses a clint server model, where the client connects to the server
and establishes a secure channel for communication.

## What security issues SSH addresses?

SSH addresses following issues:

* eavesdropping: SSH encrypts all data transmitted between the client and server. This means that even if an attacker
  intercepts the network traffic, they will only see encrypted gibberish. Consequently, sensitive information like
  passwords and data remain secure from being read by unauthorized parties
* session hijacking: Each SSH session uses cryptographic mechanisms (including integrity checksums) to ensure that the
  data has not been tampered with. An attacker trying to take over an existing session would need to generate the
  correct cryptographic checksums to maintain the session’s integrity. Since they do not possess the necessary
  cryptographic keys, they cannot forge these checksums, making it practically impossible to hijack an active session.

## SSH architecture

SSH security model leverages public/private key pairs: for example it uses asymmetric keys for:

### verify host identity

> * What It Means: When we connect to a remote SSH server, the local client needs to be sure that it’s talking to the
    legitimate host and not an imposter.
> * Mechanism:
  >   * **Host Key Pair**:
  >     * Every SSH server has a host key pair (public/private keys) generated during its initial setup (e.g., RSA, Ed25519). 
  >     * The server’s public key is shared with clients, while the private key remains securely stored on the server.

  >   * **First Connection Workflow**:
  >     * When a client first connects to a server, the server sends its public key. 
  >     * The client stores this key in a file like ~/.ssh/known_hosts (or %UserProfile%\.ssh\known_hosts on Windows). 
  >     * The client prompts the user to verify the server’s "fingerprint" (a hash of the public key) to ensure authenticity.

  >   * **Subsequent Connections**:
  >     * The client checks the server’s public key against the stored entry in known_hosts. 
  >     * If the keys match, the connection proceeds. 
  >     * If they mismatch, the client warns of a potential security breach (e.g., server impersonation or key rotation).
> * Why It’s Important: This verification step prevents attackers from impersonating the server, which is a common
    tactic in
    man-in-the-middle attacks. Without this check, the client could be sending sensitive information to an attacker’s
    machine instead of the intended server.

### set up the encrypted communication channel

> * What It Means: Establish a secure, encrypted tunnel to protect data from eavesdropping or tampering.
> * Mechanism:

>   * **Key Exchange**:
>     * During the SSH handshake, the client and server use asymmetric encryption to negotiate a shared symmetric session key. 
>     * Common algorithms include Diffie-Hellman (DH) or Elliptic Curve Diffie-Hellman (ECDH) for secure key exchange.
>   * **Hybrid Encryption**:
>     * Asymmetric keys secure the initial key exchange. 
>     * The negotiated symmetric session key (e.g., AES-256) then encrypts all subsequent data. 
>     * Symmetric encryption is faster and more efficient for bulk data transfer.
>   * **Example Workflow**
>     * Client encrypts a challenge with the server’s public key. 
>     * Server decrypts it with its private key and responds. 
>     * Both parties derive the same symmetric session key to encrypt communication.
> * Why It’s Important: This process ensures that the entire communication is encrypted. Even if someone intercepts the
    data, they won’t be able to decipher it without the symmetric key, which was securely exchanged using the
    public/private key mechanism.

### as an optional authentication method to validate connecting user

> * What It Means: Besides verifying the server’s identity, SSH can also use public/private key pairs for authenticating
    the user who is trying to log in.
> * How It Works: Users can generate their own key pairs and then place the public key on the server in a file (
    commonly ~/.ssh/authorized_keys). When the user than attempt to connect, the server challenges the user to prove
    that you possess the private key corresponding to one of the public keys it trusts. You do this by signing a piece
    of data with your private key. The server then uses your stored public key to verify the signature. This method can
    supplement or even replace traditional password authentication, providing a more secure and often more convenient
    way to authenticate.
> * Why It’s Important: Key-based authentication is typically stronger than password-based methods because it’s much
    more resistant to brute-force attacks. Additionally, it allows for more flexible access control, such as enforcing
    specific key usage policies or using different keys for different purposes.

