# How to get your Raspberry Pi ip address

After you configure your OS image and you have the SSH active, you set up your SSID and password for your home Wi-Fi to connect via SSH from WSL you need to know your Rpi IP address.

# Steps

### SSH from Windows Power Shell:

  1. Search in your search bar for Power Shell.
    
  2. Right click on it and Run as Administrator.
   
  3. Run the command: `Start-Service ssh-agent`, used to start the ssh service.
   
  4. If you try to ssh now into the RaspberryPi and you get an error that is because you didn't enabled the service status, run this command:`Set-Service -Name ssh-agent -StartupType 'Automatic'`

  5. Verify service status: `Get-Service ssh-agent`.
   
  6. Then you can finally ssh into the Rpi using the command: `ssh hostusername@raspberrypi.local`, you will be promted for a password that you set when configured the SD card.

### How to reveal your dynamic IP address

Run the commmand: `hostname -I`, be careful to be inside your Rpi bash EX: `host_username@raspberrypi:~ $`.

That's it now you know your dynamic IP for your RaspberryPi and you can ssh using `ssh host_username@ip_address`.

