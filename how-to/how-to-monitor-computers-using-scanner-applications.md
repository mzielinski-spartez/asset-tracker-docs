# How to monitor computers using scanner applications

### Overview

Asset Tracker can accept input from [WMI and SSH scanner applications](https://bitbucket.org/spartez/ephor-scanners/downloads). These applications are not only able to discover conputers and report them, but also to continuously monitor changes to these computers and report updated data.

For example, scanners can be configured to read disk usage or system uptime.

This can be done in two ways:

* each computer can have a scanner application installed, configured to periodically monitor a given parameter and to report to Asset Tracker.
* scanner can be configured to periodically connect to computers on the network, query them for a given parameter and report to Asset Tracker.

In both cases, the way to schedule scanning is by plugging into the host computer's scheduling mechanism:

* [task scheduler](how-to-import-data-from-external-sources/importing-from-scanned-computer-equipment/wmi-scanning/performing-wmi-scan-outside-of-jira.md#scheduling-scans) on Windows \(WMI scanner\)
* [crontab](how-to-import-data-from-external-sources/importing-from-scanned-computer-equipment/ssh-scanning/performing-ssh-scan-outside-of-jira.md#scheduling-scans) on LInux and Mac \(SSH scanner\)

In both cases, the scanner application is run from the command line.

The difference is that in first case \(each computer has its own scanner\), the `--self` option is used \([SSH](how-to-import-data-from-external-sources/importing-from-scanned-computer-equipment/ssh-scanning/performing-ssh-scan-outside-of-jira.md#using-command-line), [WMI](how-to-import-data-from-external-sources/importing-from-scanned-computer-equipment/wmi-scanning/performing-wmi-scan-outside-of-jira.md#using-command-line)\). In second case, the [`--ip-range`](how-to-import-data-from-external-sources/importing-from-scanned-computer-equipment/wmi-scanning/performing-wmi-scan-outside-of-jira.md#scanning-network-subnet-range) \(WMI\) or [`--range`](how-to-import-data-from-external-sources/importing-from-scanned-computer-equipment/ssh-scanning/performing-ssh-scan-outside-of-jira.md#scanning-network-subnet-range) \(SSH\) option is used.

### Configuration

The most important part of setting up the computer monitoring is configuring the scanner to monitor a particular value. The configuration depends on what you want to monitor. In examples below, we will configure scanners to monitor system uptime.

[Configuration file for WMI scanners](https://bitbucket.org/spartez/ephor-scanners/raw/214b8976d0eed672d0b6fbac1e786598f8fbb974/windows/commandline/default_wmi_config.xml) should looks like this:

```markup
<?xml version="1.0" encoding="utf-8"?>
<fields>
    <matcher field="spartez.network" updateOnly="true"
        filter="NOT ServiceName=&quot;vwifimp&quot; AND NOT ServiceName=&quot;tunnel&quot;"
    />
    <field type="single"  
        objectClass="Win32_PerfFormattedData_PerfOS_System"
        propertyName="SystemUpTime" mod="3600" assetField="custom.system.uptime"
    >{0}</field>
</fields>
```

[Configuration file for SSH scanners](https://bitbucket.org/spartez/ephor-scanners/raw/214b8976d0eed672d0b6fbac1e786598f8fbb974/unix/scanner/src/default-config.xml) should look like this:

```markup
<?xml version="1.0" encoding="UTF-8" ?>
 
<fields>
    <os type="linux" path="/bin:/sbin:/usr/bin:/usr/sbin">
        <matcher
                field="spartez.network"
                updateOnly="true"
                command="ip link list | grep \'link/\' | grep -v \'00:00:00:00:00:00\' | awk \'{print $2}\'"
        />
        <field type="single" assetField="custom.system.uptime"  scanner="proc" path="/proc/uptime" />
    </os>
    <os type="darwin"  path="/sbin:/bin:/sbin:/usr/bin:/usr/sbin">
        <matcher
                field="spartez.network"
                updateOnly="true"
                command="ifconfig | grep \'ether\' | grep -v \'00:00:00:00:00:00\' | awk \'{print $2}\'"
        />
 
        <field type="single" assetField="custom.system.uptime"  scanner="sysctl" prop="kern.boottime" />
     </os>
</fields>
```

The **`custom.system.uptime`** field used in the example is a field set up in Asset Tracker for storing uptime - you need to [define this field](../guide/defining-an-asset-field.md) in your Asset Tracker data scheme.

Note that in both cases, the **`updateOnly` **property is set to **`true` **in the **`matcher` **element. This assures that the scanner will not create new asset records - it will only update existing ones.

### Mixing discovery and monitoring

Obviously, it is possible to perform discovery and monitoring using one scheduled operation - in this case, all values to monitor must be included in the configuration file for discovery. However, the **`updateOnly`**property of the **`matcher` **element should be set to **`false`.**

