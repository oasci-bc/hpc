# SSH

Secure Shell (SSH) is a cryptographic network protocol that enables secure remote access to servers, devices, and services over an untrusted network.
SSH provides a secure communication channel between two networked devices, allowing users to authenticate, execute commands, and transfer data securely. SSH encrypts all data transmitted between the client and the server, ensuring confidentiality and integrity of the communication.

SSH was first developed in 1995 by Tatu Ylönen, a researcher at the Helsinki University of Technology, as a secure alternative to the unencrypted remote access protocols like Telnet and RSH.
Since then, SSH has become the de facto standard for remote access in Unix-like systems and is widely used in high-performance computing (HPC) environments.

SSH operates on a client-server model.
The SSH client initiates a connection to the SSH server, which listens for incoming connections on a specific port (default port 22).
The client and server then engage in a key exchange process to establish a secure communication channel.

The SSH connection setup involves the following steps:

1.  The client sends a connection request to the server, specifying the desired SSH protocol version.
2.  The server responds with its supported SSH protocol version and its public host key.
3.  The client verifies the server's public host key against its known hosts list to ensure the server's authenticity.
4.  The client and server negotiate encryption algorithms and key exchange methods.
5.  The client and server generate session keys using the agreed-upon key exchange method.
6.  The client authenticates to the server using one of the supported authentication methods (e.g., password, public-key, or keyboard-interactive).
7.  Upon successful authentication, the client is granted access to the server, and an encrypted communication channel is established.

Once the SSH connection is established, the client can execute commands on the remote server, transfer files, or create additional secure channels (e.g., port forwarding) within the encrypted SSH tunnel.

!!! note "Example"

    To connect to a remote server using SSH, you can use the `ssh` command followed by the username and the server's hostname or IP address:

    ```bash
    ssh username@hostname
    ```

    For instance, to connect to a server named `hpc-cluster.example.com` with the username `johndoe`, you would run:

    ```bash
    ssh johndoe@hpc-cluster.example.com
    ```
