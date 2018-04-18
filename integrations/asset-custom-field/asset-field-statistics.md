# Asset field statistics

The _Asset_ custom field in Jira and Service Desk can be used to generate pie charts, which show how many issues are associated with a given asset. See screenshot below for an example of such a pie chart.

![](https://confluence.spartez.com/download/attachments/34603534/pie1.png?version=1&modificationDate=1483353488194&api=v2&effects=drop-shadow)

To add a pie chart of this kind to your Jira dashboard, add a gadget of a type "Pie Chart" to the dashboard and then select "Asset" as a "Statistics Type". Of course the "Project or Saved Filter" for the pie chart can contain any valid Jira search query, letting you generate charts for various situations \(for example, "not resolved issues", "issues updated recently", etc.\).

![](https://confluence.spartez.com/download/attachments/34603534/pie2a.png?version=2&modificationDate=1483362729157&api=v2&effects=drop-shadow)

In addition to pie charts with individual assets as statistics type, you can also create charts where the "Statistics Type" is asset's [type](../../guide/creating-new-asset-type.md) or [folder](../../guide/working-with-folders.md). Values for a given slice of the pie will be calculated based on type or category of an asset set in the "Asset" custom field in your Jira issues.

![](https://confluence.spartez.com/download/attachments/34603534/pie2.png?version=1&modificationDate=1483362675253&api=v2&effects=drop-shadow)

![](https://confluence.spartez.com/download/attachments/34603534/pie3.png?version=1&modificationDate=1483362712688&api=v2&effects=drop-shadow)

To add a pie chart of this kind to your Jira dashboard, add a gadget of a type "Pie Chart" to the dashboard and then select "Asset Folder" or "Asset Type" as a "Statistics Type"

![](https://confluence.spartez.com/download/attachments/34603534/pie2a.png?version=2&modificationDate=1483362729157&api=v2&effects=drop-shadow)

