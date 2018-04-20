# Automated actions execution in Service Desk

Service Desk contains the [automation](https://confluence.atlassian.com/servicedeskcloud/automating-your-service-desk-732528900.html) feature, allowing to execute predefined actions in response to various events, like creation of the request, adding a comment and so on.

Asset Tracker provides a _THEN _rule, which plugs into this automation framework. This rule lets Service Desk automatically invoke action on an asset associated with a request. For example, this can be used to assign an asset to a requesting user, mark the asset as broken or fixed, etc.

In order to add an automation rule that modifies the asset, first pick "_Automation_" from the Service Desk project's administration menu:

![](https://confluence.spartez.com/download/attachments/36733369/sd1.png?version=1&modificationDate=1496396956464&api=v2&effects=drop-shadow)

Then click the "_Add rule"_ button \(you can also modify an existing rule\):

![](https://confluence.spartez.com/download/attachments/36733369/sd2.png?version=1&modificationDate=1496396972249&api=v2&effects=drop-shadow)

Select "_Custom rule" _\(or any other rule that is applicable in your case\):

![](https://confluence.spartez.com/download/attachments/36733369/sd3.png?version=1&modificationDate=1496396994004&api=v2&effects=drop-shadow)

Now it is time to fill in the rule dialog. You need to do three things:

1. give the rule a name
2. define the triggers \(the "_WHEN_" clause, for example "_Issue created", "Comment added",_ etc\)
3. define the actions to perform \(the "_THEN_" clause\). Here you can add an action to modify an asset

Optionally you can add an "_IF_" clause to tune the rule some more to your needs.

![](https://confluence.spartez.com/download/attachments/36733369/sd4.png?version=1&modificationDate=1496397020050&api=v2&effects=drop-shadow)

When defining the action to perform \("_THEN_" clause\), select the _"Modify asset" _from the dropdown:

![](https://confluence.spartez.com/download/attachments/36733369/sd5.png?version=1&modificationDate=1496397044699&api=v2&effects=drop-shadow)

This opens the dialog which lets you select the action to use \(only public actions are available, because the post function has to be available for all users\). You can even add a new action directly from this panel, by clicking the "_Add_" link.

![](https://confluence.spartez.com/download/attachments/36733369/sd6.png?version=1&modificationDate=1496397067818&api=v2&effects=drop-shadow)

The "_Ignore asset field operation errors" _checkbox can be used to not generate an error when the action produces an error \(for example if the value of the field to set is invalid\). If this checkbox is cleared, the error will generate entry in Service Desk error log. Otherwise, it will only produce a warning message in Jira log file.

![](https://confluence.spartez.com/download/attachments/36733369/sdlog.png?version=1&modificationDate=1496402512145&api=v2&effects=drop-shadow)

