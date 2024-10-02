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

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Top level system diagram</p></figcaption></figure>

The VotingWorks voting system (a.k.a. **VxSuite**) consists of four primary components: VxAdmin, VxMark, VxScan, and VxCentralScan.&#x20;

Using VxSuite for an election begins with generating an [election package](election-package/) and [hand marked ballots ](hand-marked-ballots.md)using an external system.&#x20;

### VxAdmin

VxAdmin is where the election administrator performs election setup tasks and manages election results. At the beginning of an election, the user configures VxAdmin with an [election package](election-package/). Once configured, VxAdmin is used for two key election setup tasks:

* Exporting a digitally authenticated copy of the election package to USB drives. The election package is used to configure VxMark, VxScan, and VxCentralScan, and it _must_ be authenticated by VxAdmin. (**insert link to authentication doc)**
* Programming role-based smart cards that will be used to authenticate on all machines. While the "System Administrator" role is election-agnostic, the "Election Manager" and "Poll Worker" roles are election-specific and cards must be programmed for every election. (**insert link to roles doc)**

VxAdmin is later used to load, store, and tabulate cast vote records from the scanners. The results are available for review or export in several results formats: PDF, comma-separated values, or Election Results Reporting CDF format. Once tabulation is complete, election administrators can mark results as official, after which no new results can be added.
