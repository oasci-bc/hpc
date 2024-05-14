# Password-based

Password-based authentication is the simplest and most straightforward method of SSH authentication.
In this method, users provide their username and password to authenticate with the remote server.

Here's how password-based authentication works:

1.  The user initiates an SSH connection to the remote server.
2.  The server prompts the user for their username and password.
3.  The user enters their credentials, which are then transmitted to the server securely over the encrypted SSH connection.
4.  The server verifies the provided credentials against the user's account information stored on the server.
5.  If the credentials are valid, the user is granted access to the server. If the credentials are invalid, the server denies access and may prompt the user to try again.

!!! note "Example"

    When using password-based authentication, the user is prompted for their password after initiating the SSH connection:

    ```bash
    $ ssh username@hostname
    Password: ********
    ```

While password-based authentication is easy to use and requires no additional setup, it has some drawbacks:

- Passwords can be weak and susceptible to brute-force attacks.
- Passwords are transmitted over the network, albeit encrypted, which can be a potential security risk if the encryption is compromised.
- Managing and updating passwords for multiple users and servers can be cumbersome and time-consuming.
