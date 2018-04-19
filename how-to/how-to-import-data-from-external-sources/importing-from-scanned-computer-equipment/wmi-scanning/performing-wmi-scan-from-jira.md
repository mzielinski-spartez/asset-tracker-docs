# Performing WMI scan from JIRA

### Installing the scanner

To scan from within Jira, the application must be installed on the computer where your Jira is located, which means that your Jira must run on Windows if you want to be able to perform discovery from within Jira. It is also possible to use the application in "standalone" mode \(not invoked from Jira\). In this mode, you need to invoke the application from Windows command line, and supply it with your Jira user credentials. See [Performing WMI scan outside of Jira](performing-wmi-scan-outside-of-jira.md) for more details.

{% hint style="info" %}
You can download the scanner application from [Bitbucket](https://bitbucket.org/spartez/ephor-scanners/downloads).

Go [here](https://bitbucket.org/spartez/ephor-scanners) for the source of the application, which is licensed under [Apache license](http://www.apache.org/licenses/LICENSE-2.0).
{% endhint %}

### Configuring the scanner

In order to set up WMI discovery in Jira, go to _Administration → WMI Discovery._** **On that page, click the "Add scanning profile" button to define scanning configuration:

![](../../../../.gitbook/assets/image%20%2819%29.png)

You are presented with a set of options, all more-less self explanatory, the most important of which is _Configuration File_, which determines what information is scanned and how it is reported. One such file, heavily commented, is bundled with the scanner application - it is appropriate for Asset Tracker's **type.computer** asset type, defined in its default data scheme. If you want to use the Tracker's default data scheme, you don't need to modify the configuration file, but you can still do it, for example to format the reported data in some other way.

![](../../../../.gitbook/assets/image%20%2825%29.png)

After you click "Save", you are ready to scan your network for Windows hosts.

![](../../../../.gitbook/assets/image%20%2851%29.png)

{% hint style="info" %}
A default XML configuration file is available in the [bitbucket repository](https://bitbucket.org/spartez/ephor-scanners/raw/214b8976d0eed672d0b6fbac1e786598f8fbb974/windows/commandline/default_wmi_config.xml). Read the comments in this file for instructions on how to customize it to your needs.
{% endhint %}

### Scanning

When you click the "Scan" button, the scanning process starts and its log is shown. Scanning runs in the background - you can close the browser and come back to it later to check progress. The whole scan can take quite a while, depending on how large your network is, how fast your computers respond and how much information you want to scan.

![](../../../../.gitbook/assets/image%20%289%29.png)

