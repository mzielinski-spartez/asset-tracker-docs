# Performing WMI scan outside of JIRA

### Scan application usage

{% hint style="info" %}
You can download the scanner application from [Bitbucket](https://bitbucket.org/spartez/ephor-scanners/downloads).

Go [here](https://bitbucket.org/spartez/ephor-scanners) for the source of the application, which is licensed under [Apache license](http://www.apache.org/licenses/LICENSE-2.0).
{% endhint %}

Running WMI scans from witin Jira requires the Jira server to be installed on a Windows host. However, it is still possible to perform WMI scans from a computer different than the one on which your Jira is located, and post scanned data to Asset Tracker, even though your Jira is on a non-Windows host.

To do this, you need to install and invoke the scanner application on a Windows host that is able to reach your Jira, after configuring it with your Jira URL and appropriate credentials. It is best to start by checking the available command line options of the scanner:  


```bash
E:\>"c:\Program Files (x86)\Spartez\Asset Tracker WMI Scanner\scanner.exe" --usage
Usage: scanner.exe [options] <jira-url>
 
    Options:
        --usage         - Print usage
        --jira-user     - Jira user name. Required if token is not supplied
        --jira-password - Jira user password. Required if token is not supplied
        --jira-token    - Security token. required if user/password is not supplied
        --folder*       - Folder path ("/" as delimiter) for new assets
        --type*         - Asset type for new assets
        --wmi-config    - WMI configuration file
        --ip-range      - Range of IP addresses to scan.
                          For example: 192.168.1.1-192.168.1.100,192.168.2.1
        --self          - only scan this computer
        --wmi-user      - WMI user account name. Use "domain\user"
                          if you need to supply domain name
        --wmi-password  - WMI user password
        --wmi-timeout   - WMI scan timeout in seconds. Default is 20 seconds
        --ping-first    - Ping the scanned machine before attempting to scan it,
                          to speed up scan of dead IP addresses
        --ping-timeout  - Ping timeout in seconds. Default is 20 seconds
        --no-close      - Don't automatically close the application console window
        --verbose       - Verbose output of scanning and updating process
        --version       - Print program version number
    (*) arguments are required
```

{% hint style="info" %}
A default XML configuration file is available in the [bitbucket repository](https://bitbucket.org/spartez/ephor-scanners/raw/214b8976d0eed672d0b6fbac1e786598f8fbb974/windows/commandline/default_wmi_config.xml). Read the comments in this file for instructions on how to customize it to your needs.
{% endhint %}

### Scanning your computer

#### Using GUI application

The most convenient way to scan your own computer is to use the "Scan My Computer" utility included in the scanner application package. This application only requires supplying Jira URL, credentials, asset folder in Asset Tracker and asset type to create, and clicking "Scan and update". Configuration has to only be performed once - the application remembers stored values \(password is stored securely\). Scan and update results are displayed in the "Update log" panel.

![](../../../../.gitbook/assets/image%20%2824%29.png)

#### Using command line {#PerformingWMIscanoutsideofJIRA-Usingcommandline}

To scan the computer that the scanner is installed on, use the `--self` option. It can be best accomplished with this batch script:

```bash
set BATCH="c:\Program Files (x86)\Spartez\Asset Tracker WMI Scanner\scanner.exe"
set Jira_USER=username
set Jira_PASSWORD=password
set FOLDER=Electronics/Computers
set TYPE=type.computer
 
%BATCH% ^
 --jira-user=%Jira_USER%^
 --jira-password=%Jira_PASSWORD%^
 --folder=%FOLDER%^
 --type=%TYPE%^
 --self^
 https://jira.url
```

Such batch script can be used by individual users to scan their own computers, without a need to provide credentials, either manually, or periodically \(see below\).

### Scanning network subnet range

The convenient way to invoke the scanner is a batch script, which can look like this \(replace credentials and IP ranges with values appropriate for your environment\):

```bash
set BATCH="c:\Program Files (x86)\Spartez\Asset Tracker WMI Scanner\scanner.exe"
set Jira_USER=username
set Jira_PASSWORD=password
set WMI_USER=domain\user
set WMI_PASSWORD=password
set FOLDER=Electronics/Computers
set TYPE=type.computer
set IP_RANGE=192.168.157.1-192.168.157.100
 
%BATCH% ^
 --jira-user=%Jira_USER%^
 --jira-password=%Jira_PASSWORD%^
 --wmi-user=%WMI_USER%^
 --wmi-password=%WMI_PASSWORD%^
 --folder=%FOLDER%^
 --type=%TYPE%^
 --ip-range=%IP_RANGE%^
 --ping-first=true^
 --ping-timeout=1^
 https://jira.url
```

### Scheduling scans

With the network scanning script ready and tested, you can make Windows run it automatically at specified times. The simplest way to do it is by using Task Scheduler.

To do this, go to "Control Panel → Administrative Tools → Task Scheduler". In it, click the "Create Basic Task" link:

![](https://confluence.spartez.com/download/attachments/34604458/tasksch.png?version=1&modificationDate=1486027111559&api=v2&effects=drop-shadow)



A multi-step dialog opens, where you can set up the task with the required parameters:

![](https://confluence.spartez.com/download/attachments/34604458/new1.png?version=1&modificationDate=1486027199501&api=v2&effects=drop-shadow)

![](https://confluence.spartez.com/download/attachments/34604458/new2.png?version=1&modificationDate=1486027215080&api=v2&effects=drop-shadow)

![](https://confluence.spartez.com/download/attachments/34604458/new3.png?version=1&modificationDate=1486027229884&api=v2&effects=drop-shadow)

![](https://confluence.spartez.com/download/attachments/34604458/new4.png?version=1&modificationDate=1486027244857&api=v2&effects=drop-shadow)

![](https://confluence.spartez.com/download/attachments/34604458/new5.png?version=1&modificationDate=1486027279932&api=v2&effects=drop-shadow)

After the last step, open the task properties and set the task up so that it can run even if nobody is logged in:

![](https://confluence.spartez.com/download/attachments/34604458/new7.png?version=1&modificationDate=1486027403332&api=v2&effects=drop-shadow)

