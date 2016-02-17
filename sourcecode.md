#source code for the mandingo's sandbox malware analysis platform

# Hello! #

These are all the required files I can provide you to run the Mandingo Sandbox :)

### [sinjector\_exe](https://code.google.com/p/mandingo/source/browse/#svn%2Ftrunk%2Fsinjector%2Fsinjector_exe) ###
  * Executable file and source code used to inject the prepared DLL into processes that are going to be analyzed.
  * Runs inside a windows guest operating system
  * Can be executed as an stand-alone program; requires the DLL to inject compiled and some configuration

### [dlltoinject](https://code.google.com/p/mandingo/source/browse/#svn%2Ftrunk%2Fsinjector%2Fdlltoinject) ###
  * DLL that will be injected in every process analyzed and each subprocess called.

### [sinjector\_client](https://code.google.com/p/mandingo/source/browse/#svn%2Ftrunk%2Fsinjector%2Fsinjector_client) ###
  * This application should be copied at your host system (mine is macosx).
  * Its function is to stablish communications between the host operating system and the virtual machine (windows running with virtualbox).
  * Provide a serie of scripts used to parse the results of the executable samples analyzed

### [webgui](https://code.google.com/p/mandingo/source/browse/#svn%2Ftrunk%2Fsinjector%2Fwebgui) ###
  * Web interface used to submit the malware samples to the virtual machine; ease of use of all the laboratory.

## More ##
If you want, read the [config](https://code.google.com/p/mandingo/source/browse/trunk/sinjector/sinjector_client/CONFIG) file supplied with the "sinjector\_client" application and get some tips for the system setup... but in my opinion, it's preferable to read the documentation provided in the [wiki page](https://code.google.com/p/mandingo/wiki/MandingoSandbox) :)