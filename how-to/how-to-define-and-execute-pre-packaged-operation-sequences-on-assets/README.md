# How to define and execute pre-packaged operation sequences on assets

Stored operation sequences are configurable sets of operations that you can perform on asset fields. The can be used to automate modifying asset records in Asset Tracker in response to events such as issuing a Sevice Desk request or scanning asset label.

These operation sequences can be invoked in a variety of ways:

* [manually](https://confluence.spartez.com/display/AT4J/Invoking+operation+sequences+manually)
* automatically from Jira [workflow post-function](https://confluence.spartez.com/display/AT4J/Automated+operation+sequences+execution+in+JIRA)
* automatically from [Service Desk "if-then" automation](https://confluence.spartez.com/display/AT4J/Automated+operation+sequences+execution+in+Service+Desk)
* from the Asset Tracker's [mobile application](https://confluence.spartez.com/display/AT4J/Invoking+operation+sequences+by+scanning+asset+label) when the asset label is scanned

One operation sequence can contain multiple operations, setting many asset fields in one go.

Operation sequences can set asset fields to predefined values, as well as modify existing values:

* increase or decrease a numeric value by specific amount
* append a text to a text field
* set a date field by a specific time interval from the time of operation execution

Operation value definitions can contain special temple markers to be filled during operation sequence execution. See [special markers](https://confluence.spartez.com/display/AT4J/Defining+operation+sequences#Definingoperationsequences-Specialmarkers) for more information.

