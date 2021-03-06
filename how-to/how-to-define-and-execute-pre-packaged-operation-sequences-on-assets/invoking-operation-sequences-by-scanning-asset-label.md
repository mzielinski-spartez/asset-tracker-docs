# Invoking operation sequences by scanning asset label

### Introduction

Asset Tracker provides [iPhone and Android applications](../../mobile-access/label-scanners.md) which let you quickly scan [asset labels](../how-to-print-labels-for-assets.md).

Scanning the label with this application automatically updates the asset record by performing a selected [operation sequences](./).

### Setting up label scanning profile in the mobile application

To actually run the inventory check, you need the [Android or iPhone application](../../mobile-access/label-scanners.md). The application is simple to use. It lets you define "Scan Profiles", which determine your Jira URL and credentials, and the operation sequence to execute when the QR code is scanned. To define the profile, pick the "_Add operation sequence profile"_ menu entry after clicking the "+" button \(you can also add the profile that [sets date field](../how-to-perform-inventory-checks.md) from that menu\):

{% tabs %}
{% tab title="Android" %}
| ![](../../.gitbook/assets/image%20%2813%29.png) | ![](../../.gitbook/assets/image%20%2857%29.png) |
| --- |
{% endtab %}

{% tab title="iPhone" %}
| ![](../../.gitbook/assets/image%20%2834%29.png) | ![](../../.gitbook/assets/image%20%286%29.png) |
| --- |
{% endtab %}
{% endtabs %}

### Scanning QR code label to execute the operation sequence

Once you set up the profile, you can press the "Scan" button to execute the selected operation sequence:  


{% tabs %}
{% tab title="Android" %}
![](../../.gitbook/assets/image%20%2844%29.png)
{% endtab %}

{% tab title="iPhone" %}
![](../../.gitbook/assets/image%20%2839%29.png)
{% endtab %}
{% endtabs %}

Scanning is fully automated - when the QR code is identified, the operation sequence is automatically executed on the asset record in Asset Tracker. 

{% tabs %}
{% tab title="Android" %}
![](../../.gitbook/assets/image%20%2811%29.png)
{% endtab %}

{% tab title="iPhone" %}
![](../../.gitbook/assets/image%20%2827%29.png)
{% endtab %}
{% endtabs %}

