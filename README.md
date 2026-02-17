# Secure SSH & Python Virtual Environment on Raspberry Pi

SSH setup and Python virtual environment configuration for Raspberry Pi remote development.

### Project architecture

In this project:

The remote host is a Raspberry Pi.

The main (client) machine is a Windows PC.

SSH connections are initiated from WSL (Windows Subsystem for Linux) running on the Windows machine.

For learning purposes, I installed Windows Subsystem for Linux (WSL), Debian distro, on my Windows machine in order to use a Linux environment and run native Linux commands. However, a different distro preference can be slected, but in the same distro family which is in my case Debian, or using a proper Linux machine also work just fine. 

Although the host operating system is Windows, all SSH commands are executed from within the WSL Linux terminal.

## Setting up SSH on Raspberry Pi

### General knowledge

Secure Shell (SSH) is a network protocol that provides a secure connection between two machines. It allows users to execute commands remotely, transfer files, and securely access systems over unsecured networks such as public WiFi or internet cafés.

SSH encrypts all communication, protecting against eavesdropping and data interception.

To connect to a remote machine via SSH, an internet connection is not strictly required. However, both machines must be connected to the same network or otherwise wouldn't be able to reach each other. This is why configuring a static IP address can be useful, as it ensures the device’s address does not change and remains accessible on the network.

### SSH activation RaspberryPi

SSH can be enabled on a Raspberry Pi when the OS image is first written to the SD card.

**Option 1**: Enable SSH from the imager using the configuration menu.

### Best practice

Configure the SSID and the passowrd for your home Wi-Fi inside the configuration menu of the imager, in this way when the RPi will boot it will connect automatically to your home Wi-Fi and you can start using it headless from the beginning.

**Option 2**: Enable SSH by opening RaspberryPi configurations menu (For more information visit: https://www.raspberrypi.com/documentation/computers/configuration.html)

Run the command: `sudo raspi-config`

1. Navigate using arrow keys to “Interface Options”.

2. Select SSH and choose Enable.

3. Exit the configuration tool and reboot if necessary.

### WSL

If Windows Subsystem for Linux installation is needed, the official documentation can be followed:

_https://learn.microsoft.com/en-us/windows/wsl/install_

### OpenSSH

Once inside the WSL command line interface, in order to SSH into the RPi it is needed to install openssh-client package using the command

`sudo apt install openssh-client`.

Then to connect via SSH run: 

`ssh host_username@host_ip`

The user will be prompted for a password that was set during the configuration of the OS image for the Rpi.

The host_username is the username set in the configuration menu for the Rpi.

In order to use the host_ip please check [GetyouripGuide](docs/GetyouripGuide.md) .

More info can be found by accesing the official documentation: _https://wiki.debian.org/SSH._

## SSH keys

To benefit the most and to properly secure your data for your SSH server generating SSH keys can be a good solution and easier than just promting the user each time.

Always the SSH keys will be generated on the client machine, the one that you want to SSH from.

When generating ssh keys the user will get a private key and a public key. The private key should be kept safe and never shared, as an extra precaution 2FA authentification can be added.

Generating the keys is as simple as running this command:

`ssh-keygen`

After running the command the keys can be saved with a name choosen by the user and they will  be a pair: choosen_name & choosen_name.pub.

### Starting the SSH server

On the remote_host the server will run and the client will try to access it using the keys, in order to do that it is needed to install the openssh-server by running the command:

`sudo apt install openssh-server` 

**!!!Caution of the machine that you are running the command to be the remote_host!!!**

After server installation the ssh connection status can be checked by running the command:

`systemctl status ssh`

Output:

<img width="298" height="28" alt="image" src="https://github.com/user-attachments/assets/8a329b76-2336-4209-bb0e-015f7e762bdb" />

### Configuration of the SSH server

At this moment the server is not configured properly in order to benefit of all the ssh keys features and to do that it is needed to acces the config files of the server.

  1. Installing a text editor that is designed for terminal use like Neovim, this tool helps with editing of the configs files like in this case.

 `sudo apt install neovim` to install the tool.

  2. To acces the server configuration file run:

`sudo nvim /etc/ssh/sshd_config`

Terminal interface should look like this:

<img width="1908" height="965" alt="image" src="https://github.com/user-attachments/assets/8a16e270-b710-4309-8583-6261d149b4a6" />

  3. The following configurations should be modified to no for seecurity reasons, especially the password authentitication because SSH keys will be used from now on.

<img width="541" height="26" alt="image" src="https://github.com/user-attachments/assets/fae9f953-fd6c-41f9-be3b-a36470512e26" />


<img width="314" height="20" alt="image" src="https://github.com/user-attachments/assets/93ddedca-9c1c-47c3-9504-23af63a94008" />


Disabling root login improves security by blocking direct SSH access to the most privileged account and reducing exposure to brute-force attacks.


### Sharing SSH keys between devices

Now that the server is up and running the public key should be shared to the server.

Inside WSL terminal, where the keys were created, the following command should be used:

`ssh-copy-id -i ~/.ssh/your_key.pub remote_host_username@remote_host_ip`

This command will copy the public key from WSL to the remote machine in the ~/.ssh/authorized_keys.

The system will ask the user to try and log in using the command:

`ssh -i /home/your_username/.ssh/your_key 'remote_host_username@remote_host_ip'` 

**Caution in this case _your_key_ is the private key !**

Now the user have acces via SSH using SSH keys, and the user is prompted everytime when the SSH connection takes place for the passphrase choosen when creating the keys.

To boost productivity and to get rid of the repeated passphrase input the following document can be checked [AddKeyToSshAgent](docs/AddKeyToSshAgent.md) .

## Virtual Environment Setup

For each project, a dedicated Python virtual environment keeps dependencies isolated from the system Python. This avoids conflicts between projects, allows installation without sudo, and makes the project portable and easy to manage. On Raspberry Pi, this approach is safer and cleaner than installing packages system-wide from my experience.

For a detailed step-by-step guide on creating and activating a Python virtual environment, check out [CreatingVirtualEnvironment](docs/CreatingVirtualEnvironment.md) .

**A practical example of running script can be checked here**

## Conclusions

This project demonstrates how to securely configure remote development on a Raspberry Pi using SSH and Python virtual environments. By separating responsibilities between the remote host (Raspberry Pi) and the client machine (Windows + WSL Debian), it establishes a clean workflow that mirrors real-world Linux development environments.

Using SSH key-based authentication significantly improves security compared to password-based login, while disabling password authentication further hardens the server. Managing keys from the client machine ensures proper security practices and controlled access.

Running SSH from WSL provides a real Linux experience on Windows, making the setup close to a proper Linux machine. The same approach works with other Debian-based distributions or a full Linux system.

Finally, using a dedicated Python virtual environment for each project ensures dependency isolation, avoids system-wide conflicts, and keeps the Raspberry Pi stable and maintainable.

Overall, this setup provides a secure, scalable, and reproducible foundation for Raspberry Pi remote development.











