# Searching for JIRA issues with assets

You can use a custom field to specify an Asset Tracker asset associated with a given issue. 

This custom field is searchable - which means that you can specify its value as a Jira search query \(JQL\) criterion.

The image below shows Jira issues searched for based on assets associated with them.

![](https://confluence.spartez.com/download/attachments/34603499/jql.ss.png?version=1&modificationDate=1480074351798&api=v2)

There are two ways in which you can specify an asset to be searched for, when searching for Jira issues:

* you can provide numerical asset IDs and use JQL **=**, **in **and **is **operators \(asset IDs are the last part of the asset URL in Jira\).   For example, you can say:  _    Asset = 10090_ _    Asset in \(10090, 10091\)     Asset is empty_ _    Asset is not empty_  The downside of this method is that you need to know the IDs of assets that you are looking for
* you can also use Asset Tracker queries \(see [Search query syntax](search-query-syntax/)\) to specify what asset to find:   For example, you can say:  _    Asset ~ "my laptop"_ _    Asset = "category = Computers"_ _    Asset = "type = type.computer"_ or _Asset = "type = Computer"_ _    Asset = "system.title ~ \"network card\""_         note the escaped quotes - they are needed if you are searching for multiple words. Alternatively, you can use single and double quotes: _Asset = "system.title ~ 'network card'"_  This method is very flexible and gives you the ability to apply full power of Asset Tracker search to finding Jira issues with associated assets.

In addition to being able to search for issues asociated with assets, you can also generate statistics graphs for them. See [Asset field statistics](../integrations/jira-asset-field/asset-field-statistics.md) for more details.

