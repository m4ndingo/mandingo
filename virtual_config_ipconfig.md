#setting the IP address of the guest operating system

# Introduction #

You need to configure an static IP for the operating system, so we can communicate the host (macosx/linux) with the [server application (server.pyw)](server_py.md) that will be running and listening in the guest os (windows)


# Details #

Start the guest os (windows xp sp3) and go to "control panel" > "networking" > "local area connection" > "properties" > "TCP/IP" and set:

  * IP address: 192.168.56.201
  * Subnet mask: 255.255.255.0
  * Default gateway: 192.168.56.1
  * DNS server: 8.8.8.8

The default gateway will be used to allow connections between the guest os (windows) and Internet. This is interesting since we want to see how the malware connects to C&C, download files, etc.

We will need to add some rules to the host os (macosx/linux) to forward this connections. This will be commented in the [forwarding connections](ip_forwarding_config.md) page.

You can continue here: [Enabling internet connectivity in the guest os](ip_forwarding_config.md)