# Configure VxMark

{% hint style="info" %}
The following steps must be completed by an Election Manager.
{% endhint %}

Before you configure VxMark, you must setup the machine. Follow [VxMark Hardware Setup](vxmark-hardware-setup.md) steps.

To configure **VxMark**, you must do two things:

1. [Save the election package](../vxadmin-system-setup/save-election-package.md) to a USB drive.
2. [Create an Election Manager Card](../vxadmin-system-setup/programming-cards.md).

## Ports

Under the accessible controller is the smartcard reader and the USB port. To access the USB port, open the metal cover.  Seal and document as required.&#x20;

<div>

<figure><img src="../.gitbook/assets/VxMark remove controller.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/VxMark card reader and USB drive.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/VxMark usb port exposed.png" alt=""><figcaption></figcaption></figure>

</div>

## Loading The Election Package

An unconfigured machine will prompt you to insert an Election Manager Card to log in and then a USB drive with the election package saved from VxAdmin to configure.&#x20;

After the USB drive is inserted, VxMark will automatically begin loading all ballot styles for the election. After the election package is done loading, the Election Manager Settings screen will display in Test Ballot Mode.

<div>

<figure><img src="../.gitbook/assets/VxMark insert EM to configure.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/VxMark insert USB with election pkg.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/VxMark configured test mode.png" alt=""><figcaption></figcaption></figure>

</div>

## Setting Mode

Use the toggle button to switch between _`Test Ballot Mode`_ and _`Official Ballot Mode`_. The machine must be in Official Ballot Mode on Election Day.  Review the [L\&A Overview instructions](../logic-and-accuracy-pre-election-testing/l-and-a-overview.md) to understand which mode to use during L\&A testing.

<figure><img src="../.gitbook/assets/image (4).png" alt="" width="188"><figcaption></figcaption></figure>

## Remove Election Data & Configuration

To remove election configuration (and all data) from VxMark:

* [ ] Insert an Election Manager Card
* [ ] Select _`Unconfigure Machine`_.

<figure><img src="../.gitbook/assets/image (5).png" alt="" width="188"><figcaption></figcaption></figure>

* [ ] Confirm by selecting _`Yes, Delete Election Data.`_

<figure><img src="../.gitbook/assets/image (158).png" alt="" width="188"><figcaption></figcaption></figure>

You can now re-configure VxMark with a different election package.
