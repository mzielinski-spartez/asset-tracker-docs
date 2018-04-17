# WMI scanning

WMI Scanner is a Windows application that scans computers on the network using [WMI](https://en.wikipedia.org/wiki/Windows_Management_Instrumentation) and securely reports the information about them to Asset Tracker.

{% hint style="info" %}
You can download the scanner application from [Bitbucket](https://bitbucket.org/spartez/ephor-scanners/downloads).

Go [here](https://bitbucket.org/spartez/ephor-scanners) for the source of the application, which is licensed under [Apache license](http://www.apache.org/licenses/LICENSE-2.0).
{% endhint %}

To scan from within Jira, the application must be installed on the computer where your Jira is located, which means that your Jira must run on Windows if you want to be able to perform discovery from within Jira. It is also possible to use the application in "standalone" mode \(not invoked from Jira\). In this mode, you need to invoke the application from Windows command line, and supply it with your Jira user credentials. See [Performing WMI scan outside of Jira](performing-wmi-scan-outside-of-jira.md) for more details.

The application attempts to connect to all MS Windows hosts on network ranges configured in scanning profiles. When the host responds, WMI scan is performed for data corresponding to configured asset type fields. Then the application updates Asset Tracker with this data, either creating a new computer asset, or updating one, depending on whether the asset with MAC address matching the scanned one exists in any known computer assets.

*  [Performing WMI scan from JIRA](performing-wmi-scan-from-jira.md)
*  [Performing WMI scan outside of JIRA](performing-wmi-scan-outside-of-jira.md)

### Required network and security configuration {#WMIscanning-Requirednetworkandsecurityconfiguration}

In order for WMI scanning to work, computers that are to be scanned must be configured to:

* allow remote reading of WMI data
* user configured for scanning must have appropriate permissions
* firewall rules must be applied

Note that this is not necessarily the default configuration, especially if your computers are not memebers of a Windows domain. Please consult these links for more information:

* [http://stackoverflow.com/a/38905171](http://stackoverflow.com/a/38905171) - how to set up remote WMI access
* [Microsoft documentation](https://msdn.microsoft.com/en-us/library/aa394603%28v=vs.85%29.aspx) - how to set up firewall and access permissions

