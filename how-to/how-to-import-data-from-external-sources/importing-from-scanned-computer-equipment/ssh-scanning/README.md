# SSH scanning

SSH Scanner is Python application that scans computers on the network using shell commands invoked over SSH connection and securely reports the information about them to Asset Tracker. The application assumes that it is operating in environments, where the following command are available \(which more-less means that it assumes some type of a Unix system, such as Linux or macOS\):

* `python` \(version 2.6 or newer\)
* `curl`
* `ssh`
* `sshpass`

The computers to be scanned must be accessible using SSH and provide a set of shell commands which will be invoked using SSH. The exact set of commands required depends on the XML configuration file in use, but the smallest subset is:

* `ifconfig` \(macOS\)
* `sysctl` \(macOS\)
* `lshw` \(Linux. Optional, but greatly improving scan results\)
* `ip` \(Linux\)
* `cat`
* `awk`
* `grep`

{% hint style="info" %}
You can download the scanner application from [Bitbucket](https://bitbucket.org/spartez/ephor-scanners/downloads). You need to install it on the computer where your Jira is located. Packages for Debian-like systems \(Debian, Ubuntu, etc.\) and RedHat-like ones \(Fedora, SuSE, etc.\) are provided, as well as a TAR archive to be manually installed on a Linux or macOS computer,

Go [here](https://bitbucket.org/spartez/ephor-scanners) for the source of the application, which is licensed under [Apache license](http://www.apache.org/licenses/LICENSE-2.0).
{% endhint %}

To perform SSH scan from within Jira, the scanner application must be installed on the computer where your Jira is located, which means that your Jira must run on Linux. It is also possible to use the application in "standalone" mode \(not invoked from Jira\). In this mode, you need to invoke the application from Linux or macOS command line, and supply it with your Jira user credentials. See [Performing SSH Scan outside of Jira](https://confluence.spartez.com/display/AT4J/Performing+SSH+Scan+outside+of+JIRA) for more details.

The application attempts to connect to all sepcified hosts on network ranges configured in scanning profiles. When the host responds, SSH scan is performed for data corresponding to configured asset type fields. Then the application updates Asset Tracker with this data, either creating a new computer asset, or updating one, depending on whether the asset with MAC address matching the scanned one exists in any known computer assets.

* [Performing SSH scan from JIRA](performing-ssh-scan-from-jira.md)
* [Performing SSH scan outside of JIRA](performing-ssh-scan-outside-of-jira.md)

### Required network and security configuration {#SSHscanning-Requirednetworkandsecurityconfiguration}

In order for SSH scanning to work, computers that are to be scanned must be configured to:

* allow incoming SSH connections \(SSH server must be installed and switched on\)
* user configured for scanning must have their SSH public key installed on the scanned machine, or username/password SSH authentication must be enabled
* firewall rules must be applied to allow inbound traffic to port 22 \(SSH\) on scanned host
* For improved scan results, the lshw command needs to be available on your Linux hosts. Otherwise, some hardware information will not be scanned

Note that this is not necessarily the default configuration. Please consult these links for more information:

* [Installing and configure SSH server on Ubuntu Linux](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)
* [Installing and configure SSH serveron Fedora Linux](https://docs.fedoraproject.org/en-US/Fedora/15/html/Deployment_Guide/s2-ssh-configuration-sshd.html)
* [Enabling SSH \("Remote Login"\) on macOS](https://support.apple.com/kb/PH18726?locale=en_US)
* [Installing SSH keys on a Linux host](https://www.howtoforge.com/linux-basics-how-to-install-ssh-keys-on-the-shell)

