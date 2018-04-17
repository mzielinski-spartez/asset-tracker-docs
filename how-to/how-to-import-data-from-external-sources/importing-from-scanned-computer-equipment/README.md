# Importing from scanned computer equipment

Asset Tracker can receive updates about asset configuration and state from external sources, using its REST API.

Computers running Windows, Linux and macOS operating systems can be scanned using configurable scanner applications, which report to Asset Tracker. Scans can be performed both from the scanned computer, or remotely from a central location. Scanners can be launched from Jira, as well as from a different machine.

Windows computers are scanned using WMI protocol. Linux and macOS computers are scanned using SSH.

* [WMI scanning](wmi-scanning/)
* [SSH scanning](ssh-scanning/)

In addition to discovering computers and reporting them to Asset Tracker, scanner applications can also monitor already discovered computers. See How to monitor computers using scanner applications for more details.

