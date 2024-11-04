# Central Scanning

{% hint style="info" %}
The following steps must be completed by the Election Manager.
{% endhint %}

VxCentralScan is a central scanning solution that allows you to quickly scan large batches of ballots. If you are using VxScan at your precincts, you can use VxCentralScan to scan absentee or vote by mail ballots on Election Day and mail, provisional, military ballots, or other ballots counted post-election day. VxCentralScan can also be used to quickly verify a test deck and retabulate an out of balance precinct.&#x20;

Follow the [VxCentral Scan Hardware Setup](vxcentralscan-hardware-setup.md) instructions to prepare the system for use.

## Scan Ballot Batches

Before scanning the first ballot batch, confirm that VxCentralScan displays No ballots have been scanned. If not,  select _`Delete All Batches`_ to clear the scanner.

<figure><img src="../user-manual/.gitbook/assets/image (916).png" alt="" width="266"><figcaption></figcaption></figure>

Load a stack of ballots into the feeder tray of the scanner. VotingWorks recommends loading no more than 30 ballot sheets at time for Fijitsu model 8170 and 100 ballot sheets for Fijitsu model 7600. The ballots need to be in a neat stack, unfolded and lying flat, but ballots can be in any orientation (e.g. upside down or backwards is fine).

Select _`Scan New Batch`_. Ballots feed through the scanner automatically and the number of ballots scanned will increase as each ballot is scanned under Ballot Count. A timestamp will appear under the Finished At header when a batch is done scanning.&#x20;

<div>

<figure><img src="../user-manual/.gitbook/assets/vxcs scan new batch.png" alt="" width="266"><figcaption></figcaption></figure>

 

<figure><img src="../user-manual/.gitbook/assets/vxscan scan ballots details screen.png" alt="" width="266"><figcaption></figcaption></figure>

</div>

Once the batch finishes scanning, remove it from the output tray on the scanner and place the next stack of ballots in the feeder tray. Repeat the scanning process until all ballots are scanned.

{% hint style="warning" %}
If a batch needs to be rescanned, use the _`Delete`_ button to remove the original scan.
{% endhint %}

## Adjudicate Ballots

VxCentralScan will stop scanning and present a review screen if scanning cannot be completed due to a blank sheet, overvoted or undervoted contest, scan mode mismatch, or an otherwise unreadable ballot sheet. The review screen will display an image of the scanned ballot sheet, the reason why scanning was stopped, and confirm that this ballot sheet has not been tabulated yet.

### Blank & Overvoted Ballots

If the scanner stops, remove the last ballot sheet scanned from the scanner output tray and confirm it matches the ballot sheet displayed onscreen. Once removed, follow review requirements. If the ballot needs to be reviewed by someone not operating the scanner or needs to be duplicated to be tabulated properly, select _`Remove to Adjudicate`_ and confirm that the _`Ballot has been removed`_. Once confirmed, the scanner will resume scanning ballots in the batch. &#x20;

##

The example below shows an **Overvote** detected that is being removed for review.

<figure><img src="../user-manual/.gitbook/assets/image (917).png" alt="" width="269"><figcaption></figcaption></figure>

A similar central review interface may be shown for other adjudication reasons depending on your election configuration including:

* Blank Ballot
* Undervote

### Unreadable Ballots

VxCentralScan may show an **Unreadable** ballot screen for a properly marked ballot if it's unable to decode ballot information due to page skew, dust, or tampering of the ballot. When a ballot sheet is shown as unreadable, you can safely remove the ballot and re-scan the ballot sheet. If the ballot is unreadable on a second scan, you should remove the ballot for duplication.

<figure><img src="../user-manual/.gitbook/assets/image (918).png" alt="" width="265"><figcaption></figcaption></figure>

### Mode Mismatch

A mode mismatch error will appear if the scanner mode (Test or Official) does not match the ballot type (Test or Official) and the scanned sheet will not be tabulated. In these cases, you should either remove the ballot from the stack or switch scanner modes.

### Saving Cast Vote Records (CVRs)

When all ballot batches (including any duplicated ballots) have been scanned, you will need to save the CVRs from VxCentralScan to load into VxAdmin for tabulation.

To save, select _`Save CVRs`_ in the top right.

<figure><img src="../user-manual/.gitbook/assets/image (919).png" alt="" width="266"><figcaption></figcaption></figure>

You'll be prompted to insert a USB drive. Once recognized, select _`Save`_ and then _`Eject USB.`_

<div>

<figure><img src="../user-manual/.gitbook/assets/image (187).png" alt="" width="188"><figcaption><p>Select Save</p></figcaption></figure>

 

<figure><img src="../user-manual/.gitbook/assets/image (188).png" alt="" width="188"><figcaption><p>Select Eject USB</p></figcaption></figure>

</div>

The CVRs will be saved in the cast-vote-records/ folder on the USB drive.

Once you've selected Eject USB, you'll see a prompt to _`Close`_ and may remove the USB drive.

If using multiple VxCentralScan stations, repeat for each one.

### Save Backup

After saving the CVRs, VotingWorks recommends also saving a backup of all data from the VxCentralScan station. To save a backup, navigate to the Settings menu and select _`Save Backup`_. Then navigate to the USB drive in the file dialog and save the backup .zip file. The file may take up to a few minutes to save.

<figure><img src="../user-manual/.gitbook/assets/image (920).png" alt="" width="266"><figcaption></figcaption></figure>



Once saved, select _`Eject USB`_ and remove the USB drive from VxCentralScan.

{% hint style="warning" %}
Tabulated ballots should be sealed into a secure container post-tabulation with the seal number recorded as required. Follow state guidelines to ensure proper retention.
{% endhint %}

