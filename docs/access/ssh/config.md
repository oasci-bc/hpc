# Configuration

The SSH config file is a text file that allows users to configure and customize their SSH client settings.
It provides a way to store frequently used SSH options, define aliases for servers, and streamline the SSH connection process.
By leveraging the SSH config file, users can simplify their SSH workflow, reduce typing, and enhance the security and convenience of their SSH connections.

The SSH config file is typically named `config` and is located in the user's SSH directory (`~/.ssh/config` on Unix-like systems and `%UserProfile%\.ssh\config` on Windows).
The file contains a series of directives and their corresponding values, which are applied to SSH connections that match the specified criteria.

## Common options

The SSH config file supports a wide range of configuration options.
Some of the most commonly used options include:

1.  `Host`: Defines a hostname or an alias for an SSH connection.
    It can be a specific hostname, an IP address, or a wildcard pattern.
2.  `HostName`: Specifies the actual hostname or IP address of the remote server.
    This is useful when using aliases or when the connection requires a different hostname than the one specified in the `Host` directive.
3.  `User`: Sets the default username for the SSH connection.
    This eliminates the need to specify the username each time you connect to the server.
4.  `Port`: Specifies the SSH port number to use for the connection.
    By default, SSH uses port 22, but this option allows you to connect to servers running SSH on a different port.
5.  `IdentityFile`: Specifies the path to the private key file to use for authentication.
    This option is useful when you have multiple keys for different servers or when the key is stored in a non-default location.
6.  `PreferredAuthentications`: Sets the order of authentication methods to try during the SSH connection process.
    This option allows you to prioritize certain authentication methods, such as publickey or password.
7.  `ServerAliveInterval`: Specifies the interval in seconds between sending keep-alive messages to the server.
    This option helps prevent the SSH connection from being dropped due to inactivity.
8.  `ServerAliveCountMax`: Sets the maximum number of keep-alive messages sent without receiving a response before the SSH connection is considered broken.
9.  `Compression`: Enables or disables compression for the SSH connection.
    Compression can improve performance on slow networks but may increase CPU usage on the client and server.

!!! note "Example"

    Here's an example of an SSH config file with some common options:

    ```text
    Host example
        HostName example.com
        User johndoe
        Port 2222
        IdentityFile ~/.ssh/example_key
        PreferredAuthentications publickey
        ServerAliveInterval 60
        ServerAliveCountMax 30
        Compression yes
    ```

In this example, the `Host` directive defines an alias `example` for the server `example.com`.
The `User` directive sets the default username to `johndoe`, and the `Port` directive specifies the SSH port as `2222`.
The `IdentityFile` directive points to the private key file `example_key` in the user's SSH directory.
The `PreferredAuthentications` directive prioritizes public-key authentication. The `ServerAliveInterval` and `ServerAliveCountMax` directives configure keep-alive settings, and the `Compression` directive enables compression for the connection.

## Setting up aliases

One of the most powerful features of the SSH config file is the ability to define aliases for frequently accessed servers.
By setting up aliases, users can connect to servers using simple and memorable names instead of typing the full hostname or IP address each time.

To set up an alias, users can add a `Host` directive followed by the desired alias name.
They can then specify the actual hostname or IP address using the `HostName` directive.

!!! note "Example"

    Consider the following SSH config file:

    ```text
    Host web
        HostName 192.168.1.100
        User webadmin
        Port 22

    Host db
        HostName 192.168.1.200
        User dbadmin
        Port 2222
    ```

In this example, two aliases are defined: `web` and `db`.
The `web` alias points to the server with IP address `192.168.1.100`, and the `db` alias points to the server with IP address `192.168.1.200`.
Each alias also specifies the corresponding username and SSH port.

With these aliases in place, users can connect to the servers using the simplified commands:

```bash
ssh web
```

or

```bash
ssh db
```

Instead of typing the full IP addresses and usernames each time.

## Configuring SSH to use specific keys for different servers

The SSH config file allows users to specify different private keys for different servers.
This is useful when users have multiple keys or when they need to use specific keys for certain servers.

To configure SSH to use a specific key for a server, users can add the `IdentityFile` directive under the corresponding `Host` block in the SSH config file.

!!! note "Example"

    Consider the following SSH config file:

    ```text
    Host web
        HostName 192.168.1.100
        User webadmin
        IdentityFile ~/.ssh/web_key

    Host db
        HostName 192.168.1.200
        User dbadmin
        IdentityFile ~/.ssh/db_key
    ```

    In this example, the `web` alias is configured to use the private key file `web_key`, and the `db` alias is configured to use the private key file `db_key`.
    Both key files are stored in the user's SSH directory.

    With this configuration, when users connect to the `web` server using the `ssh web` command, SSH automatically uses the `web_key` for authentication.
    Similarly, when connecting to the `db` server using the `ssh db` command, SSH uses the `db_key` for authentication.

    This setup allows users to maintain separate keys for different servers, enhancing security and flexibility in their SSH connections.

!!! note "Example"

    To generate a new SSH key pair for a specific server, users can use the `ssh-keygen` command with the `-f` option to specify the filename:

    ```bash
    ssh-keygen -t rsa -b 4096 -f ~/.ssh/web_key
    ```

    This command generates a 4096-bit RSA key pair, with the private key saved as `web_key` and the public key saved as `web_key.pub` in the user's SSH directory.

    Users can then copy the public key to the server using the `ssh-copy-id` command:

    ```bash
    ssh-copy-id -i ~/.ssh/web_key.pub webadmin@192.168.1.100
    ```

    After copying the public key, users can add the corresponding `IdentityFile` directive to their SSH config file to associate the private key with the server.
