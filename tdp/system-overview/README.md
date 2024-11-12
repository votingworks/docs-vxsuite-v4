---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# System Overview

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption><p>Top level system diagram</p></figcaption></figure>

The VotingWorks voting system (a.k.a. **VxSuite**) consists of four primary components: VxAdmin, VxMark, VxScan, and VxCentralScan.&#x20;

Using VxSuite for an election begins with generating an [election package](election-package/) and [hand marked ballots ](hand-marked-ballots.md)using an external system.&#x20;

## VxAdmin

VxAdmin is where the election administrator performs election setup tasks and manages election results. At the beginning of an election, the user configures VxAdmin with an [election package](election-package/). Once configured, VxAdmin is used for two key election setup tasks:

* Exporting a copy of the election package to USB drives with a digital signature. The election package is used to configure VxMark, VxScan, and VxCentralScan, and it _must_ be digitally signed by VxAdmin. (**insert link to authentication doc)**
* Programming role-based smart cards that will be used to authenticate on all machines. While the "System Administrator" role is election-agnostic, the "Election Manager" and "Poll Worker" roles are election-specific and cards must be programmed for every election. (**insert link to roles doc)**

VxAdmin is later used to load, store, and tabulate cast vote records from the scanners. The results are available for review or export in [several results formats](vxadmin-results-exports/). Once tabulation is complete, election administrators can mark results as official, after which no new results can be added.

* [vxadmin-function.md](vxadmin-function.md "mention")
* [vxadmin-hardware.md](vxadmin-hardware.md "mention")

## VxMark

VxMark is the system's ballot-marking device (BMD) that provides an accessible voting experience. At the beginning of an election, it is configured with an election package from VxAdmin. Once configured, a voter can make vote selections in various interaction modes according to their needs. The following input modes are supported:

* Touch, using the touchscreen
* Tactile, using the accessible controller
* Limited Dexterity, using a sip-and-puff device or equivalent

The following output modes are supported:

* Visual, with options to change color contrast and text size
* Audio, with navigation instructions and contest details read to the user over headphones

The voter can also adjust the language to any language with translations specified in the election package.&#x20;

After finishing with selections, the a [machine marked ballot](machine-marked-ballots.md) is printed and presented to the voter. The ballot is scanned (but not cast) so the interpreted results can be presented to the voter on-screen. After reviewing the ballot and confirming their selections, the ballot is cast and ejected into the attached ballot box. At a later time, depending on election procedures, the ballot will be removed from the ballot box and tabulated at one of the system's scanners.

* [vxmark-function.md](vxmark-function.md "mention")
* [vxmark-hardware.md](vxmark-hardware.md "mention")

## VxScan

VxScan is the system's precinct scanner. At the beginning of an election, it is configured with an election package from VxAdmin which specifies the ballot layouts. The polls are opened by a poll worker after which casting ballots is allowed. Opening polls prints a tally report which is empty because no ballots have been scanned, a.k.a. the zero report.&#x20;

Voters cast ballots by inserting their ballots into the scanner in any orientation. After interpreting the scanned ballot, the scanner will drop the ballot into the ballot box and inform the voter their ballot was successfully cast. If the election is configured to support adjudication reasons (e.g. overvotes) and the ballot triggers an adjudication reason, the scanner will hold the ballot while the voter is notified of the issues on their ballot and chooses whether to cast their ballot or return it to update or spoil. During voting, VxScan is continuously exporting CVRs to an attached USB drive.&#x20;

When polls are closed, the CVR export is completed and a polls closed report prints. The polls closed report includes the vote tallies of all ballots cast at the scanner while polls were open. Unlike the vote tallies eventually exported from VxAdmin, the vote tallies at VxScan do not contain any adjudication information such as write-in adjudication. The CVR export on the USB drive is then taken to VxAdmin for adjudication, aggregation, and reporting.

* [vxscan-function.md](vxscan-function.md "mention")
* [vxscan-hardware.md](vxscan-hardware.md "mention")

## VxCentralScan

VxCentralScan is the system's batch scanner, often used to scan absentee or provisional ballots. At the beginning of an election, it is configured with an election package from VxAdmin which specifies the ballot layouts.&#x20;

Ballots are inserted in the batch scanner's hopper and a batch scan is triggered from VxCentralScan. The ballots are scanned and interpreted in succession until the hopper is empty. If a ballot triggers a configured adjudication reason (e.g. it has an overvote) scanning will pause and the ballot will be displayed on screen, at which point the user can choose to tabulate the ballot anyway or remove it, untabulated.

After scanning is complete, the user can export the CVRs to a USB drive and take the USB drive to VxAdmin for adjudication, aggregation, and reporting.

* [vxcentralscan-function.md](vxcentralscan-function.md "mention")
* [vxadmin-hardware.md](vxadmin-hardware.md "mention")
