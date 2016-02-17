#how to share the network connection for the guest os (windows) using the "host only interface" in **macintosh**

# Introduction #

Follow this steps to share the internet connection of you **mac** with the virtualized guest os (windows xp)


# Steps #

Edit the file /etc/pf.conf:

```
$ sudo vim /etc/pf.conf
```

Add the following line before "nat-anchor":

```
nat on en0 from vboxnet0:network -> (en0)
```

Save the file.

Reload the configuration with:

```
sudo pfctl -f /etc/pf.conf
sudo pfctl -e
```

Enable IP forwarding with:

```
sudo sysctl -w net.inet.ip.forwarding=1
```

That's it. If you go to your guest os (windows xp virtual machine) you should have internet connectivity.

Open a "cmd.exe" console and try "ping google.com" (or browse some web page) to check it.

# share\_inet\_hostonly\_macosx.sh #

There's also an script provided with sinjector with the instructions [here](https://code.google.com/p/mandingo/source/browse/trunk/sinjector/sinjector_client/scripts/share_inet_hostonly_macosx.sh)

Note: if you restart your host system, you will need to reenable IP forwarding for get connectivity in the guest machine. You can get the commands again running the "share\_inet\_hostonly\_macosx.sh" script again. Ex:

```
$ sudo ./share_inet_hostonly_macosx.sh 
Password:
net.inet.ip.forwarding: 0 -> 1
Edit /etc/pf.confg and add the following line belowe nat-anchor:
nat on en0 from vboxnet0:network -> (en0)
Reload: sudo pfctl -f /etc/pf.conf
Enable: sudo pfctl -e
$ sudo pfctl -f /etc/pf.conf
pfctl: Use of -f option, could result in flushing of rules
present in the main ruleset added by the system at startup.
See /etc/pf.conf for further details.

No ALTQ support in kernel
ALTQ related functions disabled
MacBook-Pro-de-seagate:scripts seagate$ sudo pfctl -e
No ALTQ support in kernel
ALTQ related functions disabled
pf enabled
$
```
You can continue here: [Sinjector guest installation](sinjector_guest_install.md)