# Clients

SSH clients are available for various operating systems, allowing users to connect to remote servers from their preferred platforms. Some popular SSH clients include:

## OpenSSH

[OpenSSH](https://www.openssh.com/) is the most widely used SSH implementation and is pre-installed on most Unix-like systems (Linux, macOS, BSD).
It provides the `ssh` command-line utility for connecting to remote servers.

!!! note "Example"

    To connect to a remote server using OpenSSH, open a terminal and run:

    ```bash
    ssh username@hostname
    ```

## PuTTY

[PuTTY](https://www.putty.org/) is a free and open-source SSH client for Windows.
It provides a graphical user interface (GUI) for configuring and managing SSH connections.

!!! note "Example"

    To connect to a remote server using PuTTY:

       - Launch the PuTTY application.
       - Enter the hostname or IP address of the remote server in the "Host Name" field.
       - Select "SSH" as the connection type.
       - Click "Open" to initiate the SSH connection.

## Windows Subsystem for Linux (WSL)

[WSL](https://ubuntu.com/desktop/wsl) allows running a Linux environment directly on Windows, providing access to the OpenSSH client.

!!! note "Example"

    To connect to a remote server using OpenSSH in WSL:

       - Open the WSL terminal.
       - Run the `ssh` command followed by the username and hostname:

     ```bash
     ssh username@hostname
     ```

## Terminal (macOS)

macOS includes a built-in terminal application that provides access to the OpenSSH client.

!!! note "Example"

    To connect to a remote server using the Terminal on macOS:

       - Open the Terminal application.
       - Run the `ssh` command followed by the username and hostname:

    ```bash
    ssh username@hostname
    ```
