# Importing from a CSV file

Asset Tracker allows importing data about your assets from a CSV file. The CSV file format required is quite simple and all the steps for successfully importing data are described below.

### Description of the process

In order to import a CSV file into Asset Tracker, you have to do the following:

1. prepare a data schema \(assets and field types, and field layouts in assets\)  required for your needs. You may start from the provided default data schema and modify it to your needs, or you can start from scratch
2. prepare a CSV file
3. import the prepared CSV file

### Preparing the CSV file

You need to prepare a separate CSV file for each of your asset types. You can prepare the file using a spreadsheet program or using any other means.

The first row of the CSV file must contain cells which contain "dotted" field type names \(see image below\). These field type names must match the dotted names defined in Asset Tracker.

![](../../.gitbook/assets/image%20%2840%29.png)



CSV file example:

![](../../.gitbook/assets/image%20%2833%29.png)



The best way to create a skeleton CSV file is to export data from Asset Tracker asset browser:

![](../../.gitbook/assets/image%20%2856%29.png)



The best way to get all fields' dotted names is to select "All fields" in the dialog that is popped up:

![](../../.gitbook/assets/image%20%2848%29.png)



The CSV file does not need to contain all fields for a given asset type. Absent fields will be left empty in the imported assets.

Subsequent rows of the CSV file should contain actual data to be imported.

### Importing the CSV file

In order to import the prepared CSV file go to _Administration-&gt;Import/Export-&gt;Import Data_:

![](../../.gitbook/assets/image%20%2825%29.png)

There, you need to specify what item type you want to import, the separator character and the format used in date/time fields. The allowed formats for date/time are defined [here](http://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html). A typical date format would be something like:

* _**yyyy-MM-dd**  _     \(year-month-day\)
* _**yyyy-MM-dd HH:mm:ss **_    \(year-month-day hour:minutes:seconds\)

You can also specify a _Key field. _If you do, then assets that have the matching value of the field to the value in CSV file will be updated with values from CSV data, instead of new asset being created.

Once you specify the above, click _Upload CSV File_ to import your data.

