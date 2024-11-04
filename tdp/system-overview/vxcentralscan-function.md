# VxCentralScan Function

VxCentralScan is the system's batch scanner which enable election managers to efficiently scan large batches of ballots.

## Configuration

VxCentralScan is configured with a signed [election package](election-package/#election-definition) exported from VxAdmin. The election definition includes the ballot layouts necessary for interpreting ballots and the system settings which indicate what type of ballot issues (e.g. overvotes) require adjudication. After the election package is loaded by an authenticated election manager, no further configuration is required.

{% hint style="info" %}
**User Manual Reference:** [Configure VxCentralScan](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxcentralscan/configure-ballot-scanner "mention")
{% endhint %}

### Ballot Mode

After initial configuration, VxCentralScan is in test ballot mode. The election manager can toggle between test ballot mode and official ballot mode. In official ballot mode, only official ballots can be scanned and exported CVRs will be official ballot CVRs. In test ballot mode, only test ballots can be scanned and exported CVRs will be test ballot CVRs. If `allowOfficialBallotsInTestMode` is set in the [system settings](election-package/#system-settings), official ballots will be allowed in test mode but exported CVRs will still be test CVRs.

Switching between ballot modes clears all scanned ballot data. The election manager can switch from test ballot mode to official ballot mode at any time. When in official ballot mode after ballots have been scanned, the election manager can only switch back to test ballot mode if the scanned ballot data has been backed up.&#x20;

### Unconfiguring

VxCentralScan can be unconfigured by an election manager or system administrator. If ballots have been scanned in official ballot mode, an election manager can only unconfigure the machine after scanned ballot data has been backed up. System administrators can unconfigure the machine at any time.

## Batch Scanning

### Scanner Management

VxCentralScan is compatible with the Ricoh fi-8170 and Ricoh fi-7600 production scanners. Once either scanner is detected, the user may begin scanning batches. The scanners are controlled via commands provided by the Debian `sane` package ("Scanner Access Now Easy") which creates a uniform API for most commercial scanners. As a result, no scanner-specific drivers are required.

### Batch Management

When the user triggers a batch scan, the scanner will start a batch and begin scanning sheets one a time. The scanner will pull the paper through and transfer a scanned image to the application which will then [interpret the ballot](ballot-interpretation.md) according to the current election definition. If any issues are found with the ballot - either the ballot is incompatible or the marks trigger some adjudication reason - scanning will pause and the election manager will be prompted to remove or tabulate the ballot. When pausing for adjudication, the batch is not yet ended. Once the election manager addresses the ballot, scanning will continue until there are no more ballots in the hopper to be scanned. At that point, the batch will end.

The start time, end time, size, and index of all batches is tracked and displayed to the election manager. If a mistake was made in organizing batches or adjudicating a ballot, election managers can delete any individual batch or delete all batches.

{% hint style="info" %}
**User Manual Reference:** [Scan Ballot Batches](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxcentralscan/scanning-ballots#scan-ballot-batches "mention")
{% endhint %}

### Imprinting

Both Ricoh scanners can be used with an optional imprinter - the fi-819PRB for the fi-8170 and the fi-760PRB for the fi-7600. As the ballot exits the scanner, the imprinter prints an identifier on the side margin of the ballot. The identifier is the batch's UUID (assigned at random at the start of the batch) suffixed with the index of the sheet in the batch e.g. `378f6a69-62d3-4184-a1a7-3a5d90083e21_0000` for the first sheet in a batch. The identifier will appear in the CVR as the `BallotAuditId`. Imprinting allows later reconciling CVRs to ballots such as in ballot comparison audits.

## Ballot Issues & Adjudication

Batch scanning pauses whenever a ballot is not counted for any reason. Sometimes the ballot was not interpreted or cannot be accepted, in which case the ballot must be removed:

* **Vertical Streaks Detected** - the scanner may require cleaning&#x20;
* **Wrong Ballot Mode** - test ballots in official ballot mode or official ballots in test ballot mode
* **Wrong Election** - the hash on the ballot does not match the currently configured election
* **Unreadable** - the ballot image could not be successfully interpreted, possibly because it is not a valid ballot or because the image skew was too great

In other cases, the ballot requires adjudication. The adjudication reasons for VxCentralScan are set in the [system settings](election-package/#system-settings) as `centralScanAdjudicationReasons` and map to the following:

* **Overvote** - at least one contest is overvoted
* **Undervote** - at least one contest is undervoted
* **Blank** - all contests are blank

In these cases, the affected contests will be highlighted on screen to the election manager and they will have the option to remove or tabulate the ballot.&#x20;

{% hint style="info" %}
**User Manual Reference:** [Adjudicate Ballots](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxcentralscan/scanning-ballots#adjudicate-ballots "mention")
{% endhint %}

## Exporting CVRs

CVRs must be exported onto a USB drive and taken to VxAdmin for aggregation and reporting. The election managers has options to either save CVRs or save a backup. When saving CVRs, ballot images are only included for ballots with write-ins and rejected ballots are not included. A backup is simply a CVR export with images for all ballots and images for rejected ballots.

After ballots are interpreted, their images are saved to disk and their interpretation is stored in VxCentralScan's data store. On export, all CVRs are pulled from the data store, converted to the CVR CDF, and written to the USB drive.&#x20;

{% hint style="info" %}
**User Manual Reference**: [Saving Cast Vote Records (CVRs)](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxcentralscan/scanning-ballots#saving-cast-vote-records-cvrs "mention")
{% endhint %}

