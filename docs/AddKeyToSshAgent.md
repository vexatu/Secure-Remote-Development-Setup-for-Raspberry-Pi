# Using the SSH agent

To avoid entering the SSH key passphrase every time you connect, you can use ssh-agent.

ssh-agent stores your decrypted private key securely in memory after you enter the passphrase once. 

This allows future SSH connections to authenticate automatically without repeated prompts.

1. Start the agent:

`eval $(ssh-agent -s)`

2. Adding the key:

`ssh-add ~/.ssh/your_key`

3. Test:

`ssh-add -l`

`ssh host_username@host_ip`

The user will be promted just once for the passphrase then the SSH connection will be much easier.

That's it.
