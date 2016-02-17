#Uploading malware samples from the web gui

# Introduction #

In this section were going to download a malware sample (you can choose other you have locally stored) and upload it to our Sandbox laboratory using the web gui.


# Some sources for Malware samples #

There're lot of places in Internet for downloading malware samples. By the moment and for demonstration purposes, I'm going to fetch a "zbot" from zeus tracker.

Open your browser and grab one binary from here: https://zeustracker.abuse.ch/monitor.php?browse=binaries

It's interesting to download a malware sample (zbot) that it's online (red color). That means that the C&C (Command and Control) server it's responding; or should be. So, we can generate a ".pcap" file with the network traffic for better understanding of that malware.

I'm going to download the sample with MD5 hash "9d8c4d9d189d5220d10223b2089efa60" for this demonstration.

Save the file locally (do not run it!), and open the web gui if ready; installation of the web gui was covered here: [Installing the Web GUI under MAMP](https://code.google.com/p/mandingo/wiki/host_webgui)

# Uploading the sample #

Open the web gui with your favorite web browser pointing to http://127.0.0.1 if this is the location where it's running; this was covered in the section:

You should see a page like this:

![https://mandingo.googlecode.com/svn/trunk/screenshots/sinjector/webgui/webgui_home.png](https://mandingo.googlecode.com/svn/trunk/screenshots/sinjector/webgui/webgui_home.png)

Click on "choose file", locate the previously downloaded file -the "zbot" from zeustracker or any other sample you'd like to analyze-, and press the button "submit sample".

If all it's ok, you should see a response page like this:

![https://mandingo.googlecode.com/svn/trunk/screenshots/sinjector/webgui/webgui_sample_uploaded.png](https://mandingo.googlecode.com/svn/trunk/screenshots/sinjector/webgui/webgui_sample_uploaded.png)

Also, if you browse with a terminal console to your local files, you should see that the uploaded file is placed in the web gui "uploads" folder:

```
$ ls -l uploads/
total 456
-rw-r--r--  1 seagate  admin  232376 15 feb 10:18 9d8c4d9d189d5220d10223b2089efa60.bin
```

Now, you are ready to analyze the sample.

You can continue here: [Analyzing samples from the web gui](webgui_analyzing_samples.md)