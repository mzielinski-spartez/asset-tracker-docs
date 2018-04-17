# How to synchronize users

### Introduction

Asset Tracker is able to retrieve users from Jira and create an asset of a specified type. This lets you extend the information about a user in your organization to contain any information that your organization requires and associate assets with Jira users. This synchronization can be done in bulk, by scanning all users in Jira and creating "user assets" out of them. It can also happen when the user logs in to Jira and opens any Asset Tracker page. User accounts in Jira are matched with "user assets" in the Asset Tracker based on the contents of a selected field of type "user" \(see section below\).    


### Synchronization page

User synchronization is configured and performed in a rather large administartion page, which can be accessed by going to _Administration → Synchronize Users _page. The dialog contains a few sections, which will be described below:

![](https://confluence.spartez.com/download/attachments/34603704/user1.png?version=1&modificationDate=1482511827577&api=v2&effects=drop-shadow)

### Synchronization on login

When you enable this option, whenever a user accesses the Asset Tracker in Jira, an asset representing this user will be created if it does not yet exist. 

![](https://confluence.spartez.com/download/attachments/34603704/user2.png?version=1&modificationDate=1482511828792&api=v2&effects=drop-shadow)

{% hint style="warning" %}
Enabling this option affects the performance of Asset Tracker page opening, because Asset Tracker needs to perform a query of its database for user field containing the currently logged-in Jira user. If you have many assets and many Jira users, this may take some time
{% endhint %}

### User creation

In this section, you specify what asset type represents a user - by default this is the "Employee" type from teh default Asset Tracker data scheme, which folder will new users be stored in and whether to use alphabetical subfolders for users, which may be a good idea if you have very many users - navigating folders with many assets may be awkward

![](https://confluence.spartez.com/download/attachments/34603704/user3.png?version=1&modificationDate=1482511829142&api=v2&effects=drop-shadow)

### Fields

This section determines what fields from Jira user record will be synchronized to which asset fields in the Asset Tracker. Username field is mandatory, the rest is optional. 

![](https://confluence.spartez.com/download/attachments/34603704/user4.png?version=1&modificationDate=1482511829755&api=v2&effects=drop-shadow)

### Synchronization initiation

In this section, you can start the actual synchronization. Before you click the "Start Synchronization" button, you can decide what subset of users to synchronize \(for example type "a" to only sync users whose username starts from this letter\). You can also narrow down the synchronization scope to specific Jira groups. 

![](https://confluence.spartez.com/download/attachments/34603704/user5.png?version=1&modificationDate=1482511830011&api=v2&effects=drop-shadow)

