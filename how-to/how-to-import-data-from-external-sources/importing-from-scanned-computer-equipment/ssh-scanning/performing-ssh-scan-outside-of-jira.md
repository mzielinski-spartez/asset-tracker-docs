# Performing SSH scan outside of JIRA

{% hint style="info" %}
You can download the scanner application from [Bitbucket](https://bitbucket.org/spartez/ephor-scanners/downloads). You need to install it on the computer where your Jira is located. Packages for Debian-like systems \(Debian, Ubuntu, etc.\) and RedHat-like ones \(Fedora, SuSE, etc.\) are provided, as well as a TAR archive to be manually installed on a Linux or macOS computer.

GUI wrapper application for scanning your macOS computer is also available from the link above - look for the file with ".dmg" extension.

Go [here](https://bitbucket.org/spartez/ephor-scanners) for the source of the application, which is licensed under [Apache license](http://www.apache.org/licenses/LICENSE-2.0).
{% endhint %}

Running SSH scans from within Jira requires the Jira server to be installed on a Linux host. However, it is still possible to perform SSH scans from a computer different than the one on which your Jira is located, and post scanned data to Asset Tracker, even though your Jira is on a non-Linux host.

To do this, you need to install and invoke the scanner application on a Linux or macOS host that is able to reach your Jira, after configuring it with your Jira URL and appropriate credentials. It is best to start by checking the available command line options of the scanner:

```text
$ python /opt/spartez/asset-tracker-scanner/scanner.py
Usage: python /opt/spartez/asset-tracker-scanner/scanner.py [options]
Options:
 
    --usage                     Print usage
    --verbose                   Verbose scan and update operations
    --range=<value>             Address range of hosts to scan. Aither this or
                                --self must be provided
    --self                      Scan this computer only. Either this or --range must be provided
    --ssh-user=<value>          User name to connector with SSH. Either this parameter,
                                or --ssh-key-file must be provided
    --ssh-password=<value>      Password to connect with SSH
    --ssh-key-file=<value>      Identity file (private key) to use to connect with SSH.
                                Either this parameter, or --ssh-user must be provided
    --xml-config=<value>        XML configuration file containing scanner parameters.
                                If not provided, default file is used
    --ping-first                Ping host before scanning with SSH
    --ping-timeout=<value>      Ping timeout (in seconds)
   *--folder=<value>            Folder path to place newly created asset records in
   *--asset-type=<value>        Type of asset to create
   *--jira-url=<value>          Your Jira URL
    --jira-user=<value>         Jira username for updating asset record. Either it,
                                or --jira-token must be provided
    --jira-password=<value>     Jira password for updating asset record. Either it,
                                or --jira-token must be provided
    --jira-token=<value>        Jira security token for updating asset record. Either it,
                                or --jira-user and --jira-password must be provided
    --version                   Print program version number
 
(*) denote mandatory parameters
```

{% hint style="info" %}
A default XML configuration file is available in the [bitbucket repository](https://bitbucket.org/spartez/ephor-scanners/raw/214b8976d0eed672d0b6fbac1e786598f8fbb974/unix/scanner/src/default-config.xml). Read the comments in this file for instructions on how to customize it to your needs.
{% endhint %}

### Scanning your computer

#### Using GUI application

If your computer is a Mac, running OSX version 10.9 or newer, the most convenient way to scan your computer is to use a GUI application available from [Bitbucket](https://bitbucket.org/spartez/ephor-scanners/downloads/) \(look for the file with ".dmg" extension\). 

This application only requires supplying Jira URL, credentials, asset folder in Asset Tracker and asset type to create, and clicking "Scan and update". Configuration has to only be performed once - the application remembers stored values. Scan and update results are displayed in the "Update log" panel.

![](https://confluence.spartez.com/download/attachments/35192908/macapp.png?version=2&modificationDate=1498820003210&api=v2&effects=drop-shadow)

#### Using command line

To scan your own computer using commandline, use the `--self` option. It can be best accomplished with this bash script:

```bash
#!/bin/sh
 
Jira_USER=username
Jira_PASSWORD=password
FOLDER=Electronics/Computers
TYPE=type.computer
Jira_URL=http://jira.url
 
python /opt/spartez/asset-tracker-scanner/scanner.py \
--jira-user=$Jira_USER \
--jira-password=$Jira_PASSWORD \
--folder=$FOLDER \
--asset-type=$TYPE \
--self \
--ping-first \
--ping-timeout=1 \
--jira-url=$Jira_URL
```

Such a shell script can be used by individual users to scan their own computers, without a need to provide credentials, either manually, or periodically \(see below\).

### Scanning network subnet range

The convenient way to invoke the scanner is a shell script, which can look like this \(replace credentials and IP ranges with values appropriate for your environment\):

```bash
#!/bin/sh
  
Jira_USER=username
Jira_PASSWORD=password
SSH_USER=user
SSH_PASSWORD=password
FOLDER=Electronics/Computers
TYPE=type.computer
IP_RANGE=192.168.157.1-192.168.157.100
Jira_URL=http://jira.url
python /opt/spartez/asset-tracker-scanner/scanner.py \
--jira-user=$Jira_USER \
--jira-password=$Jira_PASSWORD \
--ssh-user=$SSH_USER \
--ssh-password=$SSH_PASSWORD \
--folder=$FOLDER \
--asset-type=$TYPE \
--range=$IP_RANGE \
--ping-first \
--ping-timeout=1 \
--jira-url=$Jira_URL
```

### Scheduling scans

With the network scanning script ready and tested, you can make your computer run it automatically. The easiest way to achieve it is by using a `cron` scheduller. 

See [contab manual page](http://man7.org/linux/man-pages/man5/crontab.5.html) for more information.

