# How to define and execute pre-packaged actions on assets

**Actions** are configurable sets of operations that you can perform on asset fields. The can be used to automate modifying asset records in Asset Tracker in response to events such as issuing a Sevice Desk request or scanning asset label.

These operation sequences can be invoked in a variety of ways:

* [manually](invoking-operation-sequences-manually.md)
* automatically from Jira [workflow post-function](automated-operation-sequence-execution-in-jira.md)
* automatically from [Service Desk "if-then" automation](automated-operation-sequence-execution-in-jsd.md)
* from the Asset Tracker's [mobile application](invoking-operation-sequences-by-scanning-asset-label.md) when the asset label is scanned

One Action can contain multiple operations, setting many asset fields in one go.

Actions can set asset fields to predefined values, as well as modify existing values:

* increase or decrease a numeric value by specific amount
* append a text to a text field
* set a date field by a specific time interval from the time of operation execution

Actions' definitions can contain special template markers to be filled during operation sequence execution. See [special markers](defining-operation-sequences.md) for more information.

