# How to view user assets

"User asset" is any asset that has a field of type "User" set to the given user. Also, all assets linked to this asset are considered "user's assets". To associate the "main" user asset \(representing the user themselves\) with a Jira user, you should set up [user synchronization](how-to-synchronize-users.md). You can then simply [link other assets](../guide/creating-links-between-assets.md) to this asset and they also become linked to the user.

The easiest way to browse your assets is to open the "Assets" top level menu and select "My Assets":

![](https://confluence.spartez.com/download/attachments/34604600/myr-assets.png?version=1&modificationDate=1487174614551&api=v2&effects=drop-shadow)

You can also add the "Asset Tracker Assets" dashboard gadget to your Jira dashboard. In its default configuration thi sgadget displays current user's assets.

![](https://confluence.spartez.com/download/attachments/34604600/gadget.png?version=1&modificationDate=1487174614768&api=v2&effects=drop-shadow)

As seen on the image below, you can view all your assets and their associated issues, as well as add issues for an asset:

![](https://confluence.spartez.com/download/attachments/34604600/my-assets.png?version=1&modificationDate=1487174614660&api=v2&effects=drop-shadow)

To see other user's assets you can go to the user's profile. It contains a very similar panel, listing all user's assets and their issues. 

![](https://confluence.spartez.com/download/attachments/34604600/user-assets.png?version=2&modificationDate=1487174614306&api=v2&effects=drop-shadow)

Additionally, you can use the `user_is` and `user_is_with_linked` functional searches to search for any user's assets in the asset browser.

