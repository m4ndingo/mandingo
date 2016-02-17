#required steps to install sinjector (executable, dll, configuration, server script) in the guest os

# Introduction #

The sinjector.exe and dlltoinject.dll files are required to patch the malware processes and monitor their API activity.

The technique used is commonly called "inline injection".

The DLL (dlltoinject.dll) is loaded in the main process (for example in malware.exe), and is responsible of writing a "log" file (C:\newlog.txt) which registry each monitored windows API call.

Also, if a new process is created from this main process (ex. using CreateProcess) the DLL will be injected in this new process (or running when CreateRemoteThread is called), so we can monitor each process activity called by the "suspicious" application.

# Details #

To install "sinjector" application in the guest operating system (virtualized windows xp sp3) you will need:

  * To compile the "sinjector.exe" binary from the [sinjector C sources](https://code.google.com/p/mandingo/source/browse/#svn%2Ftrunk%2Fsinjector%2Fsinjector_exe) or get the [compiled file](https://code.google.com/p/mandingo/source/browse/trunk/sinjector/sinjector_exe/sinjector.exe)
  * To compile the "dlltoinject.dll" library from the [dlltoinject C sources](https://code.google.com/p/mandingo/source/browse/#svn%2Ftrunk%2Fsinjector%2Fdlltoinject) or get the [compiled library](https://code.google.com/p/mandingo/source/browse/trunk/sinjector/dlltoinject/dlltoinject.dll)
  * Create the "**C:\sinjector**" folder in the guest operating system.
  * Create the "**C:\sinjector\injector.ini**" file with the following contents:
```
dll=dlltoinject.dll
monitor=C:\Documents and Settings\user\Desktop\watchdocs\
backup=c:\temp\
logfile=c:\newlog.text
debuglevel=0
reinject=1
reinject_blacklist=injector.exe|POIDE.exe|ctfmon.exe|pythonw.exe
```
    * Note 1: The "monitor" variable is a feature used to monitor "file writings" in some folder; not required for analyzing all malware, but present at this moment.
    * Note 2: The "backup" variable should point to a directory where the deleted files (ex. "**c:\temp**") will be saved. **You will need to create this folder** if it doesn't exists and you want to recover the deleted files.
    * Note 3: do not change the "logfile" variable. If you do that, you will need to change the source code of other scripts that are going to request this file (ex. "client.py" from "sinjector\_client", "modules/config.php" from "web gui", etc.)
    * Note 4: if you don't want to monitor a specific process by its name, add it to "reinject\_blacklist" with the following format: |name.exe
  * Copy the python server application "**server.pyw**" to "C:\sinjector". You can find this script in the sinjector\_client sources or [here](https://code.google.com/p/mandingo/source/browse/trunk/sinjector/sinjector_client/server.py)
    * Note 1: you will need to install python 2.7 to run the server.py application in the windows machine
    * Note 2: rename the file from "server.py" to "server.pyw" if you want to hide the python console.
  * Copy the files "**sinjector.exe**" and "**dlltoinject.dll**" to "C:\sinjector" folder.
> When all the applications will be copied to "C:\sinjector" folder, a "dir c:\sinjector" command should output something like this:

```
C:\sinjector>cd ..

C:\>dir c:\sinjector
 Volume in drive C has no label.
 Volume Serial Number is 84E9-BF87

 Directory of c:\sinjector

12/27/2014  08:05 PM    <DIR>          .
12/27/2014  08:05 PM    <DIR>          ..
01/15/2015  01:44 PM            53,760 sinjector.exe
02/02/2015  12:03 PM            78,336 dlltoinject.dll
12/28/2014  11:07 PM             1,653 server.pyw
02/02/2015  12:11 PM               238 injector.ini
               4 File(s)        133,987 bytes
               2 Dir(s)   1,838,514,176 bytes free
```

# Running sinjector.exe #

This step is optional, but if you want, you can run sinjector.exe as a stand-alone application and see -how it works-.

If you want to see the help, simply run "sinjector.exe" without arguments:

## sinjector.exe help ##

```
C:\sinjector>sinjector.exe
Simple DLL Injector v1.01 by mandingo - Dic, 2014
Usage         : injector <options>
Options       : /l       List processes
                /p <pid> Hook process with PID <pid> (/P if suspended)
                /x <cmd> Exec cmd (full path req.) and hook it
                /X <cmd> Exec cmd, hook it and wait for keypress
Configuration : C:\sinjector\injector.ini
 > settings   : dll=, monitor=, logfile=, iatfile=, debuglevel=
                backup=, reinject=, reinject_blacklist=
DLL Injected  : C:\sinjector\dlltoinject.dll
```

Now, let's run sinjector.exe with some program, for example "notepad.exe" and see what is the result:

```
C:\sinjector>sinjector.exe /x c:\windows\system32\notepad.exe
Simple DLL Injector v1.01 by mandingo - Dic, 2014
[Info] Launching process: c:\windows\system32\notepad.exe
[info] New pid: 11840
[info] CreateRemoteThread Injection
[info] The remote thread was successfully created
```

The "notepad" application should be shown. Now you can close it, or open some files... close the application, and see what has been logged opening the file "c:\newlog.text"

```
C:\sinjector>type c:\newlog.text
[11464 ] [injector] EXECUTING "c:\windows\system32\notepad.exe" HOOKING PID 11840
[11840 ] [GetModuleHandleA] handle=2088763392 "kernel32.dll"
...
[11840 ] [GetProcAddress] handle=2088763392 "LoadLibraryW"
[11840 ] [GetModuleHandleA] handle=16777216 "(null)"
[11840 ] [GetProcAddress] handle=0 "RegisterPenApp"
[11840 ] [RegCreateKeyExW] handle=0xc0 MAXIMUM_ALLOWED "HKCU\Software\Microsoft\Notepad"
[11840 ] [RegCreateKeyW] handle=0xc0 0x0 "HKCU\Software\Microsoft\Notepad"
[11840 ] [RegQueryValueExW] REG_DWORD REG_DWORD_LITTLE_ENDIAN "handle(0xc0)\lfEscapement" "0"
...
```

You can continue here: [Creating a working snapshot of the guest system](guest_snapshot.md)