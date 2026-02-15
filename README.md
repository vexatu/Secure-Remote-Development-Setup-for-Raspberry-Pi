# SSH-into-Raspberry-Pi-Create-a-Python-Virtual-Environment

SSH setup and Python virtual environment configuration for Raspberry Pi remote development.

## Setting up SSH on Raspberry Pi

### General knowledge

Secure Shell (SSH) is a network protocol that provides a secure connection between two machines. It allows users to execute commands remotely, transfer files, and securely access systems over unsecured networks such as public WiFi or internet cafés.

SSH encrypts all communication, protecting against eavesdropping and data interception.

To connect to a remote machine via SSH, an internet connection is not strictly required. However, both machines must be connected to the same network or otherwise wouldn't be able to reach each other. This is why configuring a static IP address can be useful, as it ensures the device’s address does not change and remains accessible on the network.

### SSH steps

SSH can be enabled on a Raspberry Pi when the OS image is first written to the SD card.

**Option 1**: Enable SSH from the imager using the configuration menu.

**Option 2**: Enable SSH by opening Raspberry-Pi configurations menu

Run the command: `sudo raspi-config`

1. Navigate using arrow keys to “Interface Options”.

2. Select SSH and choose Enable.

3. Exit the configuration tool and reboot if necessary.
