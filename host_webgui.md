#required steps to install the Web GUI under MAMP

# Introduction #

For ease to use of all the applications and elements that are part of this sandboxing system or laboratory, a web GUI has been designed and coded in PHP.

The requirements are minimal, since no database engines are needed at this moment or third party libraries.

# Web server installation #

Before running the web gui, we need to install or configure a web server that supports PHP.

I've chosen MAMP for macosx, you can find it here: http://www.mamp.info/en/

Simply, download the installation package and run it.

Now, you have to:

  * Choose a listening port (ex. 80)
  * Choose the root folder; we will put there the PHP files (ex: ~/htdocs/)

And launch the server.

Check that the server it's working ok opening the URL http://127.0.0.1/ if you are working with your local server.

# PHP Web GUI installation #

You can find the PHP files required to run the web gui [here](https://code.google.com/p/mandingo/source/browse/#svn%2Ftrunk%2Fsinjector%2Fwebgui)

Simply, download them and put it all inside the root folder that you have chosen in the previous step.

Refresh the URL http://127.0.0.1/ and that's it, you should see now the web interface for the Mandingo's Sandbox :)

![https://mandingo.googlecode.com/svn/trunk/screenshots/sinjector/webgui/webgui_home.png](https://mandingo.googlecode.com/svn/trunk/screenshots/sinjector/webgui/webgui_home.png)

# Final configuration steps #

Now, you have to edit the file "modules/config.php", that actually have the following information:

```
<?php
class Config{
    public static $python="/Library/Frameworks/Python.framework/Versions/2.7/bin/python";
    public static $sinjector_path="/Users/mandingo/python/sinjector_client";
    public static $radare2_path="/usr/local/bin";
    public static $sinjector_client="client.py";
    public static $sinjector_vm_addr="192.168.56.201";
    public static $logfilename="newlog.text";
}
?>
```

And make some changes if needed:

  * Specify a valid python binary interpreter path for the variable **$python**
  * Specify the path where your sinjector client scripts are installed; this was covered in the section: [Installing the "sinjector client"](https://code.google.com/p/mandingo/wiki/host_sinjector)
  * Specify the path where the binary "radare2" was installed
  * Specify the IP address of the guest virtual system; this was covered in the section: [Setting the guest IP address ](https://code.google.com/p/mandingo/wiki/virtual_config_ipconfig)

# Checking the web interface #

Now, we are going to check that the "samples" section it's working fine.

When we click on "samples", we should get the list of samples analyzed (0 at the beginning), and don't get any errors.

If for example, you get the following error:

```
ERROR - "/Users/mandingo/python/sinjector_client/results" not found...
#	 Sample	 Type	 Art	 Analysis	 Status
```

That means that you haven't edited properly the "modules/config.php" file, since it's pointing to a path that doesn't exists. If you find this error, please, change the following line pointing to a path where the sinjector client is installed:

```
    public static $sinjector_path="/Users/mandingo/python/sinjector_client";
```

You can get this error if the "results" folder it's not found, so make sure that exists -and have write permissions-; this was covered in the section: [Installing the "sinjector client"](https://code.google.com/p/mandingo/wiki/host_sinjector)

If all it's ok, you should now be ready to analyze malware samples using the web gui.

You continue here: [Uploading samples from the Web GUI](webgui_uploading_samples.md)