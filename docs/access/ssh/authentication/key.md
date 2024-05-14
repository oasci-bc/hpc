# Key-based

Key-based authentication, also known as public-key authentication, is a more secure and convenient alternative to password-based authentication.
In this method, users authenticate using a pair of cryptographic keys: a public key and a private key.

Here's how key-based authentication works:

1.  The user generates a pair of cryptographic keys: a public key and a private key.
2.  The public key is copied to the remote server and added to the user's `authorized_keys` file in their SSH directory (`~/.ssh/authorized_keys`).
3.  The private key is kept secure on the user's local machine and should never be shared.
4.  When the user initiates an SSH connection, the client sends a request to the server, including the user's public key.
5.  The server checks if the provided public key matches an entry in the user's `authorized_keys` file.
6.  If a match is found, the server generates a random challenge and encrypts it using the user's public key.
7.  The encrypted challenge is sent back to the client, which then decrypts it using the user's private key.
8.  The client sends the decrypted challenge back to the server, proving that it possesses the corresponding private key.
9.  If the decrypted challenge matches the original challenge, the server grants access to the user.

!!! note "Example"

    To set up key-based authentication, the user first generates an SSH key pair using the `ssh-keygen` command:

    ```bash
    $ ssh-keygen -t ed25519
    Generating public/private ed25519 key pair.
    Enter file in which to save the key (/home/alex/.ssh/id_ed25519):
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in /home/alex/.ssh/id_ed25519
    Your public key has been saved in /home/alex/.ssh/id_ed25519.pub
    The key fingerprint is:
    SHA256:5Cmo+dj6w2h08LtbMMMOEEUT+D+93I9eEd/iEh2rJFE alex@oreo
    The key's randomart image is:
    +--[ED25519 256]--+
    |.+=.      E      |
    |.. .     .       |
    |..      o . .    |
    | .o. . o o + +   |
    |  .+*.. S + = .  |
    |  .==+.. o = .   |
    | .o+.+.o  + .    |
    |  o++.o .o .     |
    | .oo*+ .o..      |
    +----[SHA256]-----+
    ```

    This generates a ED25519 key pair.
    The user then copies the public key to the remote server using the `ssh-copy-id` command:

    ```bash
    ssh-copy-id -i /home/alex/.ssh/id_ed25519 username@hostname
    ```

    After setting up key-based authentication, the user can connect to the remote server without being prompted for a password:

    ```bash
    ssh username@hostname
    ```

## Comparison

Key-based authentication offers several advantages over password-based authentication:

1.  **Enhanced security:** Cryptographic keys are much harder to guess or brute-force compared to passwords. The private key is never transmitted over the network, reducing the risk of interception.
2.  **Convenience:** Users can connect to the remote server without entering a password each time, streamlining the login process and enabling automated scripts and workflows.
3.  **Scalability:** Managing SSH keys is easier than managing passwords for a large number of users and servers. SSH keys can be centrally managed and distributed using tools like SSH agent and SSH agent forwarding.
4.  **Two-factor authentication:** Key-based authentication can be combined with other factors, such as passphrase-protected private keys or hardware security tokens, to provide an additional layer of security.
5.  **Auditing and access control:** SSH keys can be associated with specific users, making it easier to audit and control access to servers. Keys can be revoked or replaced without affecting other users.

However, key-based authentication also has some considerations:

-   **Key management:** Properly managing SSH keys, including generating, distributing, and revoking keys, requires a well-defined process and regular maintenance.
-   **Private key security:** Users must keep their private keys secure and protected. If a private key is compromised, an attacker can gain unauthorized access to the associated servers.

!!! note "Using both"

    To further secure key-based authentication, users can protect their private keys with a passphrase. When generating an SSH key pair, the user is prompted to enter a passphrase:

    ```bash
    $ ssh-keygen -t rsa -b 4096
    Enter passphrase (empty for no passphrase): ********
    Enter same passphrase again: ********
    ```

    The passphrase encrypts the private key, adding an extra layer of protection. When using a passphrase-protected private key, the user is prompted for the passphrase during the SSH connection process:

    ```bash
    $ ssh username@hostname
    Enter passphrase for key '/home/user/.ssh/id_rsa': ********
    ```

    To avoid entering the passphrase repeatedly, users can use an SSH agent to securely store the decrypted private key in memory for the duration of the session.
