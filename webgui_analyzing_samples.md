#Analyzing samples from the web gui

# Introduction #

After uploading a sample from the web gui we are ready to analyze it (if all it's working ok).

![https://mandingo.googlecode.com/svn/trunk/screenshots/sinjector/webgui/webgui_sample_uploaded.png](https://mandingo.googlecode.com/svn/trunk/screenshots/sinjector/webgui/webgui_sample_uploaded.png)

Basically, you only have to click in the "Analyze" link after submitting the sample.

# Running the analysis #

When the analysis is running properly:

  * VirtualBox should be started (popup) and the working snapshot you've configured should be opened.
  * When the snapshot get network connectivity, you should read the message "Remote port is open"

```
[info] Trying to connect to remote port (30 seconds max)...
Error(0) - timed out
Error(1) - timed out
Error(2) - timed out
[info] Remote port is open :)
```
  * After a while, the sample you want to analyze should be automatically uploaded to the virtual guest system:
```
Uploading sample (md5: 9d8c4d9d189d5220d10223b2089efa60)
Sample uploaded: C:\sinjector/binary4
```
  * tcpdump should be launched for the host only interface, and you should not get any error.
  * A initial screenshot should be taken.
  * And you should see the rest of the output of the "sinjector.exe" client -> the API monitored for the sample (malware) you have submitted.

If all it's ok, you should see an output like this:

![https://mandingo.googlecode.com/svn/trunk/screenshots/sinjector/webgui/webgui_log.png](https://mandingo.googlecode.com/svn/trunk/screenshots/sinjector/webgui/webgui_log.png)

## Viewing the results from the console ##

All the results are stored inside the folder "results"; this was commented in the section: [Installing the "sinjector client"](https://code.google.com/p/mandingo/wiki/host_sinjector)

If we access to the "sinjector client" folder using a console we can see that some files that have been created after the analysis of the sample "9d8c4d9d189d5220d10223b2089efa60" (binary MD5 hash):

```
$ ls -l results/9d8c4d9d189d5220d10223b2089efa60/
total 2952
-rw-r--r--  1 seagate  staff      24 15 feb 11:25 network.pcap
-rw-r--r--  1 seagate  staff   14513 15 feb 11:25 newlog.text
-rw-r--r--  1 seagate  staff     745 15 feb 11:24 processes.txt
-rw-r--r--  1 seagate  staff     782 15 feb 11:25 processes_final.txt
-rw-------  1 seagate  staff  450266 15 feb 11:24 screenshot-1secs.png
-rw-------  1 seagate  staff  514062 15 feb 11:25 screenshot-40secs.png
-rw-------  1 seagate  staff  514062 15 feb 11:25 screenshot-59secs.png
```

What we are seeing as output?

  * A network pcap file (probably empty / no communications)
  * A file with the output of the "sinjector.exe" application (newlog.text) / monitored API calls
  * A file which contains the processes running before uploading the sample (processes.txt)
  * A file whith contains the final processes (processes\_final.txt)
  * And three screenshots (taken at seconds 1, 40, and 59); this can be changed editing the script "client.py"

If you want, you can use the scripts located inside the "scripts" folder against those results. Example:

```
$ ./scripts/affected_processes.py results/9d8c4d9d189d5220d10223b2089efa60/newlog.text 
1604   alive        new C:\sinjector/binary4
1604   created      new C:\sinjector/binary4
```

```
$ ./scripts/loaded_libraries.py results/9d8c4d9d189d5220d10223b2089efa60/newlog.text 
handle=1983447040 "C:\WINDOWS\SYSTEM32\IMM32.DLL"
handle=1968963584 "C:\WINDOWS\SYSTEM32\MSCTFIME.IME"
handle=2089811968 "C:\WINDOWS\SYSTEM32\NTDLL.DLL"
handle=2088763392 "KERNEL32"
handle=1933705216 "MSVBVM60"
handle=2001600512 "OLE32.DLL"
handle=1997668352 "OLEAUT32.DLL"
handle=2121400320 "SXS.DLL"
handle=2118189056 "USER32"
handle=1524039680 "UXTHEME.DLL"
handle=0 "VERSION.DLL"
handle=2009071616 "VERSION.DLL"
```

## Some errors ##
### When python is not located ###

If you have not configured properly the path of the python interpreter binary in "modules/config.php" you'll get an error like this:

```
sh: /Library/Frameworks/Python.framework/Versions/2.7/bin/python: No such file or directory
```

You can try to locate the current working python binary with:

```
$ whereis python
/usr/bin/python
```

Then, edit the file "modules/config.php" present with the PHP scripts of the webgui, and replace the variable $python, so you can read this:

```
<?php
class Config{
        public static $python="/usr/bin/python";
        ...
```
### When you don't have permissions to run "tcpdump" ###
If you don't have permissions to run "tcpdump", you should read a message like this:
```
tcpdump: vboxnet0: You don't have permission to capture on that device
((cannot open BPF device) /dev/bpf0: Permission denied)
```
Tip: if you fell safe enabling global suid permissions to "tcpdump", simply run:
```
$ sudo chmod a+s /usr/sbin/tcpdump
```

### When "tcpdump" is working, but the interface host only is not in "promiscuous" mode ###

If you get an error like this:

```
tcpdump: WARNING: vboxnet0: That device doesn't support promiscuous mode
(BIOCPROMISC: Operation not supported on socket)
```

It means that your interface is not configure in "promiscuous" mode.

To enable "promiscuous" mode:

  1. Go to VirtualBox
  1. Select your guest os (windows xp sp3)
  1. Open the configuration
  1. Go to Network > Adapter 1 > Advanced
  1. And in "promiscuous" mode select "Allow All"

### Other errors ###

You may get other errors during the analysis, so I'll try to cover them when I have free time here.

Anyway, if you need some "fast support" don't hesitate to contact me :)