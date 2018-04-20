# Defining actions

### Launching actions edition dialog {#Definingoperationsequences-Launchingoperationsequenceseditiondialog}

Actions can be added and edited from a couple of places:

* from the asset's "cog" menu in asset browser:

  ![](../../.gitbook/assets/image%20%2810%29.png)

* from the "Actions" menu for the selected assets in asset browser:

  ![](../../.gitbook/assets/image%20%2830%29.png)

* from the button on the asset page:

  ![](../../.gitbook/assets/image%20%2823%29.png)

### Adding and editing actions

Invoking the Actions presents this dialog:

![](https://confluence.spartez.com/download/attachments/36733363/oplist.png?version=1&modificationDate=1496396005769&api=v2&effects=drop-shadow)

The dialog contains "_My actions_" tab and "_Public actions_" tab. Public actions can only be added and edited by Asset Tracker administrators. 

The dialog allows adding, editing and deleting actions, as well as executing them.

To add an action, click either the "_Add My Action_" or the "_Add Public Action_" button. This opens the dialog letting you define the action name:

![](../../.gitbook/assets/image%20%2847%29.png)

After you click the _Add_ button, the action edition dialog opens, which lets you define the actual operations that will be performed when the it's invoked:

![](../../.gitbook/assets/image%20%2863%29.png)

You first select the field to modify and then fill in the value that will be set. For each field type, a context-specific helpful description of allowed values and modifiers is displayed.

### Special markers

Some of the field types can be set not just hardcoded values, but also to templates, which are filled during action execution. The following templates are available:

| **Template** | **Applicable field type** | **Description** |
| --- | --- | --- | --- | --- | --- |
| $currentDate$ | text line, text area, date | Date of execution |
| $currentTime$ | text line, text area | Date and time of execution |
| $currentUser$ | text line, text area, user | User executing the action |
| $assignee$ | text line, text area, user | Assignee of the issue from which the action is invoked, or issue [uniquely associated with the asset](../../integrations/jira-asset-field/) |
| $reporter$ | text line, text area, user | Reporter of the issue from which the action is invoked, or issue [uniquely associated with the asset](../../integrations/jira-asset-field/) |

{% hint style="warning" %}
Some of the templates \(e.g. `$reporter$`\) require Asset Tracker to know what issue to use. In some cases this is obvious, for example when the action is executed from the issue page or from a workflow post-function. In other cases \(for example on the asset page\), finding out which issue to use is not necessarily trivial. Asset Tracker tries to identify which issue to use by examining which issues the asset is linked to. If it finds exactly one linked issue, it is used. Otherwise an error is generated.
{% endhint %}

### Value modifiers

Some fields can be not only set to some value, but also modified. 

| **Modifier** | **Applicable field type** | **Description** |
| --- | --- | --- | --- |
| + | text area | Appends a specified text to the existing text area field |
| + | integer, double | Adds a specified value to a numeric field. To substract a value, use the "+-" notation,  for example "`+-100" `will substract 100 from the current value |
| `+-XmYwZd` | date | Sets the value of the date field to the date of the action execution,  plus or minus a specified number of months, weeks and days. For example `+2w3d`, `-4d` |



