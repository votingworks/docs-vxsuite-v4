# Configure VxCentralScan

{% hint style="info" %}
The following steps must be completed by the Election Manager.
{% endhint %}

Before you configure VxCentralScan, you must setup the machine. Follow the steps in the [VxCentralScan Hardware Setu](vxcentralscan-hardware-setup.md)p.

To configure **VxCentralScan**, you must do two things in **VxAdmin**:

1. [Save the election package](../user-manual/vxadmin-system-setup/save-election-package.md) to a USB drive.
2. [Create an Election Manager Card](../user-manual/vxadmin-system-setup/programming-cards.md).

## Load Election Package

Once the election package is saved to a USB drive, you can load the file to VxCentralScan.

[Setup the VxCentralScan hardware](vxcentralscan-hardware-setup.md) and turn on the VxCentralScan laptop. Insert an Election Manager Card to configure VxCentralScan will be displayed.



<div>

<figure><img src="../user-manual/.gitbook/assets/image (921).png" alt="" width="262"><figcaption></figcaption></figure>

 

<figure><img src="../user-manual/.gitbook/assets/insert EM VxCS.png" alt="" width="375"><figcaption></figcaption></figure>

</div>

Using an Election Manager Card, unlock the machine. Then follow the prompt to insert the USB drive with the election package. The election package will automatically load.

<div>

<figure><img src="../user-manual/.gitbook/assets/image (152).png" alt="" width="375"><figcaption></figcaption></figure>

 

<figure><img src="../user-manual/.gitbook/assets/configure vxcw (5).png" alt="" width="375"><figcaption></figcaption></figure>

</div>

VxCentralScan is now configured and in Test Mode. The screen will show _No ballots have been scanned_ and election summary information (name, date, jurisdiction, etc.) will be shown in the bottom left corner of the screen.&#x20;

<figure><img src="../user-manual/.gitbook/assets/image (142).png" alt="" width="375"><figcaption></figcaption></figure>

VxCentralScan is now ready for scanning.&#x20;

## Remove Election

To remove an election package and reset VxCentralScan:

* [ ] Insert an Election Manager Card
* [ ] Select _`Settings`_ from the side menu
* [ ] Select _`Unconfigure Machine`_
* [ ] Confirm by selecting _`Yes, Delete Election Data`_

<div>

<figure><img src="../user-manual/.gitbook/assets/image (143).png" alt="" width="375"><figcaption></figcaption></figure>

 

<figure><img src="../user-manual/.gitbook/assets/vxcs yes delete election data.png" alt="" width="375"><figcaption></figcaption></figure>

</div>

You can now re-configure VxCentralScan with a different election package.

{% hint style="info" %}
VxCentralScan may also be unconfigured with a System Administrator Card and selecting _`Unconfigure Machine`_ from the System Administrator screen.
{% endhint %}

{% hint style="warning" %}
If at any point, the VxCentralScan laptop becomes unresponsive, simply press the power button for one second and release. Don't hold the button down. Once the laptop has shutdown, press the power button again to restart.
{% endhint %}
