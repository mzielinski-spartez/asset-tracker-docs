# Automated actions execution in JIRA

Jira contains a workflow engine, which allows executing actions when issue undergoes a state transition. This mechanism is called _workflow post function_.

Asset Tracker plugs into this mechanism and lets Jira automatically invoke action on an asset associated with a transitioned issue. For example, this can be used to assign an asset to the issue reporter when the issue is resolved, mark the asset as broken when the issue goes to the "_In progress_" state, etc.

In order to define the post function you need to edit the workflow definition. To do this:

1. go to the "_Workflows" _page of the project administration
2. find the workflow that you are interested in and click the edit button \(with the pencil icon\)

![](https://confluence.spartez.com/download/attachments/36733367/w1.png?version=1&modificationDate=1496397457370&api=v2&effects=drop-shadow)



This opens the workflow definition screen. On this screen, select the state transition that you would like to modify:

![](https://confluence.spartez.com/download/attachments/36733367/w2.png?version=1&modificationDate=1496397470401&api=v2&effects=drop-shadow)



This open the transition definition screen. On this screen, select the "_Post Functions" _tab and click "_Add post function"_

![](https://confluence.spartez.com/download/attachments/36733367/w3.png?version=1&modificationDate=1496397486659&api=v2&effects=drop-shadow)

This opens a page where you can select the type of function. Select "_Modify Associated Asset" _and click "_Add":_

![](https://confluence.spartez.com/download/attachments/36733367/w4.png?version=1&modificationDate=1496397511191&api=v2&effects=drop-shadow)

This opens a page where you can select the action to use \(only public actions are available, because the post function has to be available for all users\). You can either select one of the existing actions, or add a new one. 

![](https://confluence.spartez.com/download/attachments/36733367/w5.png?version=1&modificationDate=1496397541162&api=v2&effects=drop-shadow)

The "_Ignore asset field operation errors" _checkbox can be used to not generate an error when the action produces an error \(for example if the value of the field to set is invalid\). If this checkbox is cleared, the error will prevent transition from taking place and an error message willbe displayed. Otherwise, it will only produce a warning message in Jira log file.

After selecting the action to use, click _"Add" _button.

The post function executing the action has been added. Now you have to publish the draft of the modified workflow to apply the changes:

![](https://confluence.spartez.com/download/attachments/36733367/w6.png?version=1&modificationDate=1496397574014&api=v2&effects=drop-shadow)

