# Setting a static IP

A static IP allows the device to be easily reached by other clients or services, enables stable communication for IoT or server applications, and prevents IP conflicts that can occur with dynamic DHCP addresses.

The static IP was configured using nmcli, more details can be found on https://networkmanager.dev/docs/api/latest/nmcli.html .

Inside your RaspberryPi terminal follow the next steps:

1. Find your router IP using the command:

`ip r | grep default` --> should be the first one and should look like this: `default via router_ip dev your_connection_type` and then followed by your actual IP for the RPi.

2. Find your router name using:

`nmcli connection show` --> should be found under the NAME column (usually your routers name that you see it on your phone or PC when you want to connect to it)

3. Now the interesting part:

`sudo nmcli connectiond modify "your_router_name" \`

`ipv4.addresses 10.0.0.169 or 192.168.29.156/24 \`

`ipv4.gateway default_router_ip \`

`ipv4.dns default_router_ip\`

`ipv4.method manual`

Breakdown:

.addresses - is your static IP that you want to set for your RPi. Can be arbitrary choosen, but in the same format as your router's IP.
.gateway - is your router IP.
.dns - usually your router IP.
.method manual - tells the RPi to stop using DHCP.

4. Reboot the RPi. That's it now you should be able to SSH into your RaspberryPi using the new static IP address.
