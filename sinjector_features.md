#Mandingo's Sandbox Features

# Features #

## Main features ##

  * Source code available
  * Static and dynamic analysis
  * Windows binaries built ready for their use
  * Documentation for installation in macosx, but can be used also in linux/unix systems (work in progress)
  * Web interface (GUI) for ease to use
  * Several tools available from the command line
  * No database support required -all is stored in local files-
  * Traffic packet capture (.pcap)
  * Automatically fetch any created (dropped?) or deleted file by the sample analyzed
  * Different injection methods used:
    * "CreateRemoteThread" for handling normal processes
    * "QueueUserAPC" for handling suspended processes
  * Injection support for windows console applications
  * Sub-processes "reinjection": automatically DLL injection of new processes -or modified processes- called from the sample that is being analyzed
  * Lot of API calls traced
    * File operations: creation, renaming, deleting, copying...
    * Networking operations: http opening requests, internet connections, socket opening, dns lookup...
    * Process operations: opening, creation, writing, remote thread creation, shell operations...
    * Registry operations: creation, opening, querying, setting...
    * Library operations: loading, getting addresses...
  * Full log, compact and very compact view modes.
  * Log highlighting.
  * Very few 3rd party libraries required
  * Artistic interpretation of the sections, resources, and the detected functions in the assembly.

## Web GUI features ##

### Static analysis ###

  * **Details**: MD5, file size, file type (magic), internal compilation date, packer identification, compiler identification, version information
  * **Sections**:
    * Name, entry, pointer to raw data, size of raw data, relative percentage, virtual address, flags, entropy, section dumping (raw), etc.
    * Notifications when a section size or offset is invalid or too big.
    * Notifications when the entropy is too high or too low.
  * **Resources**:
    * Type, graphical display of bitmaps and icons, virtual address, offset to data, size, file offset, language identification, creation date, percentage, resource dumping (raw), etc.
    * Notifications when a resource size is invalid or too big.
    * .Net resources are also identified
  * **Imports**: function names, addresses, libraries, links to online documentation
  * **Strings**: unicode strings, ascii strings
  * **Graph**: graphical display if the binary. Very useful to identify compressed or encrypted parts, paddings, etc. Hexadecimal and ASCII interactive dumping of the binary data, section markers, etc.

### Dynamic analysis ###

  * **Processes**: PID, action (created, opened, written, alive...), status (new, running), process name. API log filtering by process ID.
  * **Libraries**: libraries and methods loaded at "run time"
  * **Registry** operations:
    * Writing, opening, setting and querying.
    * Important events highlighting
  * **File operations**: files created and deleted
  * **Networking**: navigate by the .pcap graphically
  * Desktop **screenshots**

### Tools ###

#### miscelaneous ####

  * pefile dump\_info()

#### monodevelop ####

  * 

#### radare2 ####

  * Information extraction:
    * binary info, entry point, imports, linked libraries, relocations, symbols, sections, strings in data section and raw strings
  * Interactive function listing and disassemble
  * Hashing

## Current list of API calls traced ##

  1. CopyFileExA
  1. CopyFileExW
  1. CopyFileA
  1. CopyFileW
  1. CreateFileA
  1. CreateFileW
  1. DeleteFileW
  1. DeleteFileA
  1. MoveFileExA
  1. MoveFileExW
  1. MoveFileA
  1. MoveFileW
  1. Sleep
  1. RegCreateKeyExA
  1. RegCreateKeyExW
  1. RegCreateKeyA
  1. RegCreateKeyW
  1. RegOpenKeyExW
  1. RegOpenKeyExA
  1. RegOpenKeyW
  1. RegOpenKeyA
  1. RegQueryValueExA
  1. RegQueryValueExW
  1. RegSetValueExA
  1. RegSetValueExW
  1. RegConnectRegistryA
  1. RegConnectRegistryW
  1. connect
  1. getaddrinfo
  1. GetAddrInfoW
  1. InternetConnectA
  1. InternetConnectW
  1. HttpOpenRequestA
  1. HttpOpenRequestW
  1. OpenProcess
  1. CreateProcessA
  1. CreateProcessW
  1. ResumeThread
  1. WriteProcessMemory
  1. CreateRemoteThread
  1. CreateProcessInternalA
  1. CreateProcessAsUserA
  1. CreateProcessAsUserW
  1. GetModuleHandleA
  1. GetModuleHandleW
  1. GetProcAddress
  1. LoadLibraryA
  1. LoadLibraryW

---

Go to main wiki [index](https://code.google.com/p/mandingo/wiki/MandingoSandbox) page