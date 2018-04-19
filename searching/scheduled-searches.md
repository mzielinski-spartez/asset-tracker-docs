# Scheduled searches

{% hint style="info" %}
In order for the scheduled queries to work, outgoing emails must be [configured correctly in Jira](https://confluence.atlassian.com/adminjiraserver/configuring-an-smtp-mail-server-to-send-notifications-947184044.html) and recipient users must have valid email addresses.
{% endhint %}

Public searches can be scheduled for background exectution. This means that once every scheduled interval, the search query will be ran over the Asset Tracker data. If the query returns more than zero results, configured users are sent an email containing these results.

![](https://confluence.spartez.com/download/attachments/34604425/mail.png?version=1&modificationDate=1485948199380&api=v2&effects=drop-shadow)

Scheduling queries is useful in various scenarios. For example:

* in environments where you collect live data \(like [wmi scans](../how-to/how-to-import-data-from-external-sources/importing-from-scanned-computer-equipment/)\) and where you would like to be notified of exceptional conditions \(e.g. hard disks getting full\)
* if you what to be notified that some expiration date \(e.g. expiration date of the license\) is approaching. In this scenario, it is useful to use r[elative date queries](search-query-syntax/), so that the periodic query is ran agains the date of its execution.

![](https://confluence.spartez.com/download/attachments/34604425/sspubedit.png?version=1&modificationDate=1485947489511&api=v2&effects=drop-shadow)

Available query schedule intervals are:

* **hourly**, with 5 min granularity
* **daily**, at a specified hour
* **weekly**, on a specified week day, at a specified hour
* **monthly**, at a specified day of the month, at a specified hour

