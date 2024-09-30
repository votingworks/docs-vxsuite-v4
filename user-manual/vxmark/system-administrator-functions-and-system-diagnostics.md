# System Administrator Functions & System Diagnostics

{% hint style="info" %}
The following steps must be completed by the System Administrator.
{% endhint %}

A few functions in VxMark are limited to System Administrators and only appear in a menu with use of a System Administrator Card.

**Reset Polls to Paused** - use the _`Reset Polls to Paused`_ function to reopen the polls. This function is most often used as a result of a poll worker error.

**Set Date & Time** - use _`Set Date & Time`_ to change the date and time.

**Reboot to BIOS** - this function is reserved for VotingWorks support staff to boot the machine into the BIOS setup screen for firmware configuration.

<figure><img src="../.gitbook/assets/image (6).png" alt="" width="375"><figcaption></figcaption></figure>

**Power Down** - select to turn off the VxMark.

**Unconfigure Machine** - select _`Unconfigure Machine`_ to delete all data and the election configuration.

**Save Log File** - select _`Save Log File`_ to save the full log of VxMark activity to the /logs folder on the inserted USB drive.

### System Diagnostics

Use the _`System Diagnostics`_ button to troubleshoot VxMark components.  If the machine is configured, you'll find the election definition, precinct, and ballot styles listed. Verify the VxMark is plugged into an External Power Supply under Power. &#x20;

The remaining diagnostics allow you to see if a device is plugged in (detected or not detected) and test the functionality.&#x20;

<figure><img src="../.gitbook/assets/image (9).png" alt="" width="375"><figcaption></figcaption></figure>

### Accessible Controller

To test the accessible controller, first make sure it is plugged in and a green check mark with detected is shown. Next, select _`Test Accessible Controller`_. Follow the instructions on the screen, pressing each button on the accessible controller when instructed.&#x20;

<figure><img src="../.gitbook/assets/image (10).png" alt="" width="188"><figcaption></figcaption></figure>

### Printer/Scanner

To test the printer/scanner, select _`Test Printer/Scanner`_.  The screen will prompt you to insert a blank sheet of paper and then show a success screen when the process is complete.  Select _`Complete Test`_ to close the page.&#x20;



<div>

<figure><img src="../.gitbook/assets/VxMark PrinterScanner Test insert sheet.png" alt="" width="188"><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/VxMark Printerscanner test succeeded.png" alt="" width="188"><figcaption></figcaption></figure>

</div>

### PAT Input (Sip & Puff)

To test or configure a Personal Assistive Technology (PAT) device, plug the device in, and select _`Test PAT Input (Sip & Puff)`_. Push a button or sip/puff to identify a Move input.  A Move input allows the user to navigate through on-screen or audio buttons.&#x20;

<div>

<figure><img src="../.gitbook/assets/VxMark PAT Test Your Device.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/VxMark Identify Move.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/VxMark Move Identified.png" alt=""><figcaption></figcaption></figure>

</div>

Next, push a different button or sip/puff to identify a Select input.  A Select input allows the user to select an on-screen or audio button. Select _`Done`_ when complete.&#x20;

<div>

<figure><img src="../.gitbook/assets/VxMark Indentify Select.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/VxMark Select Indentified.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/VxMark Device Inputs Identified.png" alt=""><figcaption></figcaption></figure>

</div>

{% hint style="warning" %}
If the same button or sip/puff is used to identify Select as was already selected for Move, the screen will say Input Triggered: "Move" - Try the the other input.&#x20;
{% endhint %}

### Front Headphone Input

To test the headphones, plug them in to the front of the VxMark, and select _`Test Front Headphone Input`_.  Select _`Play audio`_ to verify audio plays through the headphones.  When finished, select _`Sound is audible`_ to close the screen.&#x20;

<div>

<figure><img src="../.gitbook/assets/VxMark Headphone play audio.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/VxMark Headphone audio is playing.png" alt=""><figcaption></figcaption></figure>

</div>

{% hint style="warning" %}
If any test fails, try to unplug/replug in the component and try again. If the test continues to fail, restart the VxMark and try again. If both options continue to fail, a new device should be plugged in.
{% endhint %}
