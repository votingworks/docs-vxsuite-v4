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

# VxScan Polls Reports

## Polls Opened and Closed Reports

When polls open or close on VxScan, a tally report is printed. The tally report contains the pre-adjudicated tally results of all ballots scanned at the scanner.

Note the following features about the tally report header in the examples below:

* **Title** - Includes the type of the polls report and the name of the precinct, or "All Precincts" if VxScan is configured to accept ballots from all precincts
* **Subtitle** - For primary elections, includes the full party name or "Nonpartisan Contests"
* **Timestamps** - The first timestamp indicates when the poll status changed and the second indicates when the report was printed. In most cases these times are the same, but in some cases the report may be printed later.
* **Election ID** - The election ID on the report is a concatenation of the [ballot hash and the election package hash](election-package/#election-package-and-ballot-hashes) and specifies exactly which election definition and election settings that the report corresponds to
* **Certification Signatures** - The space is provided for poll workers or election officials to sign the report in accordance with local statute.

The ballot counts table will provide the count of hand marked vs. machine marked ballots. For multi-sheet elections, it will provide counts per sheet.

Contest results are organized simply with a row for candidate or option. Because results at VxScan are not yet adjudicated, all write-ins are be grouped under the "Write-In" bucket except unmarked write-ins, which will appear as undervotes until adjudicated at VxAdmin.&#x20;

As a rule, the sum of the number of votes for all candidates, the number of undervotes, and the number of overvotes will equal the number of total possible votes for the contest, which is the number of ballots times the number of selections allowed.

<figure><img src="../.gitbook/assets/image (10) (1).png" alt="" width="563"><figcaption><p>Polls opened report for a primary election</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (11) (1).png" alt="" width="563"><figcaption><p>Polls closed report for a general election in test mode</p></figcaption></figure>

## Polls Paused and Resumed Reports

When voting is paused or resumed, VxScan prints a report containing the ballot count. Tally results are never included. The metadata is structured in the same way as the polls opened and closed reports.

<figure><img src="../.gitbook/assets/image (12).png" alt="" width="563"><figcaption><p>Voting paused report</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (13).png" alt="" width="563"><figcaption><p>Voting resumed report</p></figcaption></figure>
