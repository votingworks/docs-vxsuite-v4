# Configure VxScan

{% hint style="info" %}
The following steps must be completed by an Election Manager.
{% endhint %}

Before you configure VxScan, you must set up the machine. Follow the steps in the [Poll Worker VxScan Setup Guide](../election-day-guides/vxscan-setup.md).

To configure **VxScan**, you must do two things in **VxAdmin**:

1. [Save the election package](../user-manual/vxadmin-system-setup/save-election-package.md) to a USB drive.
2. [Create an Election Manager Card](../user-manual/vxadmin-system-setup/programming-cards.md).

## Loading The Election Package

An unconfigured machine will prompt you to insert an Election Manager Card to log in and then a USB drive with the election package saved from VxAdmin to configure.&#x20;

<div>

<figure><img src="../user-manual/.gitbook/assets/image (153).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../user-manual/.gitbook/assets/image (154).png" alt=""><figcaption></figcaption></figure>

</div>

{% hint style="warning" %}
Only one USB drive should be plugged into VxScan at a time. The other USB port is designed as a backup in the event of a failure.
{% endhint %}

###

###

After you insert the USB drive, VxScan will automatically begin loading all ballot styles for the election. After the election package is done loading, the Election Manager Settings screen will display in Test Ballot Mode.

<figure><img src="../user-manual/.gitbook/assets/image (34).png" alt="" width="375"><figcaption></figcaption></figure>

Jurisdictions with more than one precinct must select the precinct for the device.&#x20;

## Setting Mode

Use the toggle button to switch between _`Test Ballot Mode`_ and _`Official Ballot Mode`_. The machine must be in Official Ballot Mode on Election Day.  Review the [L\&A Overview instructions](../logic-and-accuracy-pre-election-testing/l-and-a-overview.md) to understand which mode to use during L\&A testing.

<figure><img src="../user-manual/.gitbook/assets/image (35).png" alt="" width="375"><figcaption></figcaption></figure>

## Remove Election Data & Configuration

There are two ways to remove the election package, unconfigure the machine, and delete all data on the VxScan. \
\
To remove the election configuration (and all data) from VxScan with an Election Manager Card:

* [ ] Insert an Election Manager Card
* [ ] Select _`Unconfigure Machine`_.

<figure><img src="../user-manual/.gitbook/assets/image (36).png" alt="" width="375"><figcaption></figcaption></figure>

* [ ] Confirm by selecting _`Yes, Delete Election Data.`_

<figure><img src="../user-manual/.gitbook/assets/image (158).png" alt="" width="188"><figcaption></figcaption></figure>

To remove the election configuration (and all data) from VxScan with a System Administrator Card:

* [ ] Insert a System Administrator Card
* [ ] Select _`Unconfigure Machine`_

<figure><img src="../user-manual/.gitbook/assets/image (24).png" alt="" width="375"><figcaption></figcaption></figure>

###

* [ ] Confirm by selecting _`Yes, Delete Election Data.`_

<figure><img src="../user-manual/.gitbook/assets/image (824).png" alt="" width="188"><figcaption></figcaption></figure>

You can now re-configure VxScan with a different election package.
