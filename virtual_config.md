#Required steps for setting up the virtual guest operating system

# Introduction #

All the malware samples will be run in a virtual operating system. We need to prepare it before analyzing them.

In this pages I will show you the configuration values I choose for this laboratory configuration:

  * macosx as the host operating system
    * mamp in the host as the web server for the gui
  * windows xp sp3 as the guest operating system

# Steps #

We will cover here the following steps:

  1. [Setting up the host-only interface](virtual_config_hostonly.md) (vboxnet0 / 192.168.56.1)
  1. [Setting the guest IP address](virtual_config_ipconfig.md) (192.168.56.201)
  1. [Enabling internet connectivity in the guest os](ip_forwarding_config.md) (macosx instructions only)
  1. [Sinjector guest installation](sinjector_guest_install.md)

You can continue here: [Creating a working snapshot of the guest system](guest_snapshot.md)