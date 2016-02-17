#installing the sinjector client

# Introduction #

Here we will cover how to install the sinjector client in your host system.

The client can be used from the command line and also their tools.

At this moment, its basic operation is:

  * "start" the virtualized "windows xp sp3" taken snapshot
  * wait for connectivity with the server (server.pyw running inside the windows machine)
  * upload the binary using the server application
  * run the "C:\sinjector\sinjector.exe" and give as argument the uploaded binary
  * wait for 1 minute (this can be changed in the client.py file)
  * retrieve the log file (C:\newlog.text) , a list with the initial and final processes, and the created/deleted files
  * "pause" the virtual machine

The results will be placed in the "results" folder. Inside this folder another folder will be created whose name will be the MD5 hash function of the binary (ex: "results/053462..8954798/newlog.text")

The tools located in the "scripts" folder of the "sinjector client" application are used to parse the results that will be generated after analyzing the binaries.

# Installation #

First, get a copy of all the "sinjector client" files located [here](https://code.google.com/p/mandingo/source/browse/#svn%2Ftrunk%2Fsinjector%2Fsinjector_client).

Don't forget to create the folder "results" with write-enabled permissions for the user that runs the web server, since later will be required. Or simply add global write permissions with the following commands:

```
$ cd sinjector_client
$ mkdir results
$ chmod a+w results
```

Check that you can run python scripts, if not, install python 2.7 in your system, an try:

```
$ ./client.py 
Usage: ./client.py <host> <sample> (ex: 192.168.56.101 fileToAnalyze.ex_)
```

As you can see, the application allows to analyze binary files if all it's properly configured. Try for example running:

```
$ ./client.py 192.168.56.201 samples/somebinaryyouhaveheretoanalyze.exe
```

  * Note: the IP address used were covered in [Virtual guest operating system configuration](https://code.google.com/p/mandingo/wiki/virtual_config_ipconfig) section

If all it's working fine, the client application should "start" the virtual box machine, upload the sample, and store the results in the "results" folder.

**An important step** here is to configure some basic parameters in the "client.py" script, so use your favorite editor an update the following lines if needed:

| **variable=value** | **Description** |
|:-------------------|:----------------|
|VMACHINE="windows xp sp3"|This is the name of your virtual machine |
|SNAPSHOT="vbox\_ao" |This is the name of the working snapshot|
|HOSTONLY\_IFACE="vboxnet0"|This is the name of the host only virtual box interface|
|TCPDUMP="/usr/sbin/tcpdump"|This is the full path where you can find "tcpdump" in your system|
|SINJECTOR="C:\\sInjector\\sinjector.exe"|This is the path where the sinjector binary is installed in the guest system|
|SECONDS=60          |This is the time that the binary sample will be analyzed|

  * Note 1: VMACHINE and SNAPSHOT where covered and commented in [Creating a working snapshot of the guest system](https://code.google.com/p/mandingo/wiki/guest_snapshot) section
  * Note 2: HOSTONLY\_IFACE was covered and commented in [Setting up the host-only interface](https://code.google.com/p/mandingo/wiki/virtual_config_hostonly) section
  * Note 3: you need to add suid and execute permissions to "tcpdump" for the user that calls the "client.py" script, also from the web interface; or run: sudo chmod a+s /usr/sbin/tcpdump
  * Note 4: the SINJECTOR installation and path where covered in [Sinjector guest installation](https://code.google.com/p/mandingo/wiki/sinjector_guest_install) section

# Libraries #

First, install "pip" if required with:

```
sudo easy_install pip
```

Then, execute the following commands to install the required libraries:

```
sudo pip install yara
sudo pip install pefile
sudo pip install dpkt

```

# 3rd party applications #

Install "monodevelop" and "radare2" in your system.

  * "Monodevelop" can be easily downloaded and installed from the package located in the http://www.monodevelop.com web page.
  * You can find "radare2" in github https://github.com/radare/radare2. The installation process is very simple, if you need the instructions read [this page](host_radare2_install.md)

You can continue here: [Installing the Web GUI under MAMP](host_webgui.md)