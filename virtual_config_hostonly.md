#configuring the host only interface

# Introduction #

In this page I will tell you how to add a host only interface in VirtualBox with the configuration I used to put all the system working.

Requeriments: I assume that you have previously installed "windows xp sp3" operating system.

# Enabling the "vboxnet0" host only network #

  * Open VirtualBox
  * Go to "Preferences" > "Network" > "Host only network" > "Add" (my new assigned network name "**vboxnet0**")
    * IP: 192.168.56.1
    * Netmask: 255.255.255.0

# Adding the host only interface to the guest #

After adding the host only network to VirtualBox, you can use it in your virtual machines.

To add this interface to the guest virtual machine (windows xp sp3), you will need:

  1. Go to the VirtualBox interface
  1. Choose the guest os (windows xp sp3)
  1. Open the configuration
  1. Go to Network > Adapter 1
  1. Enable network adapter
  1. Select "host-only adapter"

The name in my case is "vboxnet0" as before; yours may be different.


Finally, you need to enable "promiscuous" mode so we can use "tcpdump" later for generating a ".pcap" file of the network traffic. To do this:

  1. Click on "Advanced"
  1. And in "promiscuous" mode select "Allow All"

You can continue here: [Setting the guest IP address](virtual_config_ipconfig.md)