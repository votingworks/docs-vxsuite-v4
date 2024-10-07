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

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Top level system diagram</p></figcaption></figure>

The VotingWorks voting system (a.k.a. **VxSuite**) consists of four primary components: VxAdmin, VxMark, VxScan, and VxCentralScan.&#x20;

Using VxSuite for an election begins with generating an [election package](election-package/) and [hand marked ballots ](hand-marked-ballots.md)using an external system.&#x20;

## VxAdmin

VxAdmin is where the election administrator performs election setup tasks and manages election results. At the beginning of an election, the user configures VxAdmin with an [election package](election-package/). Once configured, VxAdmin is used for two key election setup tasks:

* Exporting a copy of the election package to USB drives with a digital signature. The election package is used to configure VxMark, VxScan, and VxCentralScan, and it _must_ be digitally signed by VxAdmin. (**insert link to authentication doc)**
* Programming role-based smart cards that will be used to authenticate on all machines. While the "System Administrator" role is election-agnostic, the "Election Manager" and "Poll Worker" roles are election-specific and cards must be programmed for every election. (**insert link to roles doc)**

VxAdmin is later used to load, store, and tabulate cast vote records from the scanners. The results are available for review or export in [several results formats](vxadmin-results-exports/). Once tabulation is complete, election administrators can mark results as official, after which no new results can be added.

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

## VxScan

VxScan is the system's precinct scanner. At the beginning of an election, is configured with an election package from VxAdmin.

