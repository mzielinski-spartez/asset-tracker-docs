# Performing SSH scan from JIRA

### Installing the scanner

{% hint style="info" %}
You can download the scanner application from [Bitbucket](https://bitbucket.org/spartez/ephor-scanners/downloads). You need to install it on the computer where your Jira is located. Packages for Debian-like systems \(Debian, Ubuntu, etc.\) and RedHat-like ones \(Fedora, SuSE, etc.\) are provided, as well as a TAR archive to be manually installed on a Linux or macOS computer,

Go [here](https://bitbucket.org/spartez/ephor-scanners) for the source of the application, which is licensed under [Apache license](http://www.apache.org/licenses/LICENSE-2.0).
{% endhint %}

To perform SSH scan from within Jira, the application must be installed on the computer where your Jira is located, which means that your Jira must run on Linux. It is also possible to use the application in "standalone" mode \(not invoked from Jira\). In this mode, you need to invoke the application from Linux or macOS command line, and supply it with your Jira user credentials. See [Performing SSH Scan outside of Jira](performing-ssh-scan-outside-of-jira.md) for more details.

### Configuring the scanner {#PerformingSSHscanfromJIRA-Configuringthescanner}

In order to set up SSH discovery in Jira, go to _Administration → SSH Discovery._** **On that page, click the "Add scanning profile" button to define scanning configuration:

![](https://confluence.spartez.com/download/attachments/38862940/ssh-scanner-1.png?version=1&modificationDate=1498816448092&api=v2&effects=drop-shadow)

You are presented with a set of options, all more-less self explanatory, the most important of which is _Configuration File_, which determines what information is scanned and how it is reported. One such file, heavily commented, is bundled with the scanner application - it is appropriate for Asset Tracker's **type.computer** asset type, defined in its default data scheme. If you want to use the Tracker's default data scheme, you don't need to modify the configuration file, but you can still do it, for example to format the reported data in some other way. 

![](https://confluence.spartez.com/download/attachments/38862940/ssh-scanner-2.png?version=1&modificationDate=1498816448201&api=v2&effects=drop-shadow)

{% hint style="info" %}
A default XML configuration file is available in the [bitbucket repository](https://bitbucket.org/spartez/ephor-scanners/raw/214b8976d0eed672d0b6fbac1e786598f8fbb974/unix/scanner/src/default-config.xml). Read the comments in this file for instructions on how to customize it to your needs.
{% endhint %}



​After you click "Save", you are ready to scan your network for Linux or macOS hosts.

![](https://confluence.spartez.com/download/attachments/38862940/ssh-scanner-3.png?version=1&modificationDate=1498816448528&api=v2&effects=drop-shadow)

### Scanning {#PerformingSSHscanfromJIRA-Scanning}

When you click the "Scan" button, the scanning process starts and its log is shown. Scanning runs in the background - you can close the browser and come back to it later to check progress. The whole scan can take quite a while, depending on how large your network is, how fast your computers respond and how much information you want to scan.

![](https://confluence.spartez.com/download/attachments/38862940/ssh-scanner-4.png?version=1&modificationDate=1498816448635&api=v2&effects=drop-shadow)

