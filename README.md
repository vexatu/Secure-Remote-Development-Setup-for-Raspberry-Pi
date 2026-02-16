# SSH-into-Raspberry-Pi-Create-a-Python-Virtual-Environment

SSH setup and Python virtual environment configuration for Raspberry Pi remote development.

### Project architecture

In this project:

The remote host is a Raspberry Pi.

The main (client) machine is a Windows PC.

SSH connections are initiated from WSL (Windows Subsystem for Linux) running on the Windows machine.

For learning purposes, I installed Windows Subsystem for Linux (WSL), Debian distro, on my Windows machine in order to use a Linux environment and run native Linux commands.

Although the host operating system is Windows, all SSH commands are executed from within the WSL Linux terminal.

## Setting up SSH on Raspberry Pi

### General knowledge

Secure Shell (SSH) is a network protocol that provides a secure connection between two machines. It allows users to execute commands remotely, transfer files, and securely access systems over unsecured networks such as public WiFi or internet cafés.

SSH encrypts all communication, protecting against eavesdropping and data interception.

To connect to a remote machine via SSH, an internet connection is not strictly required. However, both machines must be connected to the same network or otherwise wouldn't be able to reach each other. This is why configuring a static IP address can be useful, as it ensures the device’s address does not change and remains accessible on the network.

### SSH activation Rpi

SSH can be enabled on a Raspberry Pi when the OS image is first written to the SD card.

**Option 1**: Enable SSH from the imager using the configuration menu.

### Best practice

Configure the SSID and the passowrd for your home Wi-Fi inside the configuration menu of the imager, in this way when the Rpi will boot it will connect automatically to your home Wi-Fi and you can start using it headless from the beginning.

**Option 2**: Enable SSH by opening Raspberry-Pi configurations menu (For more information visit: https://www.raspberrypi.com/documentation/computers/configuration.html)

Run the command: `sudo raspi-config`

1. Navigate using arrow keys to “Interface Options”.

2. Select SSH and choose Enable.

3. Exit the configuration tool and reboot if necessary.

### WSL

If it is needed to install Windows Subsystem for Linux can be followed the official documentation:

https://learn.microsoft.com/en-us/windows/wsl/install

### OpenSSH

Once inside the WSL command line interface, in order to SSH into the Rpi it is needed to install openssh-client package using the command

`sudo apt install openssh-client`.

Then to connect via SSH run: 

`ssh host_username@host_ip`

The user will be prompted for a password that was set during the configuration of the OS image for the Rpi.

The host_username is the username set in the configuration menu for the Rpi.

In order to use the host_ip please check [GetyouripGuide](docs/GetyouripGuide.md) .

_More info can be found by accesing the officila documentation: https://wiki.debian.org/SSH._


