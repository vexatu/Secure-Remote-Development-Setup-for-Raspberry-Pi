# Using the SSH agent

To avoid entering the SSH key passphrase every time you connect, you can use ssh-agent.

ssh-agent stores your decrypted private key securely in memory after you enter the passphrase once. 

This allows future SSH connections to authenticate automatically without repeated prompts.

Inside the client machine the following commands should run:

1. Start the agent:

`eval $(ssh-agent -s)`

2. Adding the key:

`ssh-add ~/.ssh/your_key`

3. Test:

`ssh-add -l`

`ssh host_username@host_ip`

The user will be promted just once for the passphrase then the SSH connection will be much easier.

**Caution if using WSL as a Linux machine every time the CLI is closed the ssh key stored inside the agent will be deleted. So everytime when you open WSL you should run these commands or you can use Windows OpenSSH.**

## Storing the keys in Windows OpenSSH feature

1.Run PowerShell as Administrator.



That's it.
