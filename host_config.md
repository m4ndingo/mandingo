#required steps to install an configure the host applications

# Introduction #

From this moment, I assume that you have a working windows xp sp3 virtual box snapshot ready to use, with the sinjector files installed, the server.pyw running, with the network configured, internet connectivity, and in "saved" state.

Now, we will need to install the sinjector client files and the web gui in the host.

They are a serie of scripts that should be copied in the system (mine is macosx) which will be used to:

  * "start" and "stop" the virtual guest system (windows)
  * upload the malware samples you'd like to analyze
  * capture the network traffic
  * provide a web interface for ease of use.
  * etc

First, we will proceed to install the "sinjector client" application (a bunch of scripts) and the scripts for the web page (also the "mamp" web server).

We will also install other third party applications like: mono development, radare2, peid, python, some required libraries, etc.

# Installation #

Ok, let's begin with the installation of all the required files in the host:

  * [Installing the "sinjector\_client"](host_sinjector.md)
  * [Installing the Web GUI under MAMP](host_webgui.md)

Once finished, you continue here: [Uploading samples from the Web GUI](webgui_uploading_samples.md)