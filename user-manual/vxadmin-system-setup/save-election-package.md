# Save Election Package

{% hint style="info" %}
The following steps can be completed by a system administrator or an election manager.
{% endhint %}

## Save Election Package

To configure VxScan, VxCentralScan, and VxMark you must first save the election package from VxAdmin to a USB drive. Select Election from the side menu in VxAdmin and select _`Save Election Package`_.

<figure><img src="../.gitbook/assets/image (131).png" alt="" width="375"><figcaption></figcaption></figure>

If you don't already have a USB drive inserted, you'll be prompted to insert a USB drive. After inserting a USB drive, you will be prompted you to save the election package. Select _`Save`_.

<figure><img src="../.gitbook/assets/save-election-package-modal.jpg" alt="" width="375"><figcaption></figcaption></figure>

VxAdmin will save an election package to the USB drive inside the `/election-packages` folder.

{% hint style="warning" %}
The election package saved at VxAdmin is different from the election package used to configure your VxAdmin. VxMark, VxScan, and VxCentralScan can only be configured with election packages saved at VxAdmin.
{% endhint %}

Once the file is saved, VxAdmin prompts you to eject the USB drive. Select _`Eject USB`_.

![](../.gitbook/assets/election-package-saved-modal.jpg)

After a few seconds, VxAdmin will confirm USB was ejected and that it is safe to remove the USB drive.

