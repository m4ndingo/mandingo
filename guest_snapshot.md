#required steps to prepare a working windows snapshot

# Introduction #

In this section I will tell you how to configure a working snapshot for analyzing the malware samples.


# Instructions #

A woking snapshot requires:

  * That you have installed a "windows xp sp3" virtual box imagen running with:
    * Networking enabled (host-only)
    * Internet connectivity (using the host-only interface)
    * All the "sinjector" required files copied in the folder "C:\sinjector":
      * sinjector.exe
      * dlltoinject.dll
      * injector.ini
      * server.pyw
    * All this steps were covered in the section [Virtual guest operating system configuration](virtual_config.md)

If the previous requirement was completed, you are almost ready to take the snapshot.

## Preparing the guest for malware analysis ##

For getting precise results about the malware behavior, it's important that, before taking the snapshot, disable any program that may interfere the analysis in this guest system like:

  * Antivirus and firewalls
  * Not important services and applications
  * Scheduled tasks, etc.

## Launching the python server script inside the guest ##

Now, you should launch the python server application called "**server.pyw**" located at "C:\sinjector", double clicking on it. If you've installed python 2.7 and the application runs fine, open the "task manager" and verify that there's a "python.exe" process running on the guest system.

## Taking the snapshot ##

Ok, now all it's ready to take the snapshot. Go to:

"VirtualBox VM" menu > "Machine" > and click on "Take Snapshot...".

VirtualBox will prompt you for a "Snapshot Name", at this moment, mine is "**vbox\_ao**"; remember it or check it when needed in the snapshots section for this operating system in VirtualBox.

Also, you will need to write, check, or remember the name of the virtual machine you are running, mine is "**windows xp sp3**"; you can read this value in the title of your running VM or in the main window of VirtualBox.

## Resume ##

At this moment, you should have :

  1. a "**windows xp sp3**"
  1. with an snapshot called "**vbox\_ao**"
  1. in "**saved**" state
  1. with the process "server.pyw" launched
  1. the sinjector files in "C:\temp"
  1. IP address properly configured, internet connectivity, etc.

Almost ready for submitting and analyzing malware samples with the Mandingo's Sandbox :)

You can continue here: [Install the host applications and configuring it](host_config.md)