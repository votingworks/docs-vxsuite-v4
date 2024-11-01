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

# Ballot Count Reports

Ballot count reports contain no contest results, only ballot and ballot sheet counts.

Whereas in tally reports, each group corresponds to a subsection of the report, in ballot count reports, each grouping corresponds to a row in the table. The ballot counts are broken down by ballot type - hand marked (HMPB), machine marked (BMD), and manual if applicable. If there are multi-sheet ballots, the hand marked ballot counts may have sheet counts specified. The count of the first sheet of each ballot style is considered the ballot count.

In the follwing example, the ballot counts are grouped by both precinct and voting method:&#x20;

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt="" width="563"><figcaption><p>Ballot count report grouped by precinct and voting method</p></figcaption></figure>

The following metadata columns may appear in a ballot count report table in order to specify groupings:

<table><thead><tr><th width="177">Header</th><th>Values</th></tr></thead><tbody><tr><td>Precinct</td><td>The name of the precinct</td></tr><tr><td>Ballot Style</td><td>The internal identifier of the ballot style</td></tr><tr><td>Party</td><td>The short name of the party, e.g. "Democrat". Included by default if the ballot style is included, in a primary</td></tr><tr><td>Voting Method</td><td>"Precinct", "Absentee", or "Provisional"</td></tr><tr><td>Scanner ID</td><td>The serial number of the scanner. Included by default if the batch is included</td></tr><tr><td>Batch</td><td>The label for the batch, or "Manual Tallies" for manually entered data</td></tr></tbody></table>

Filters apply to the entire report and are specified in the title for a simple filter or are specified by attribute below the title for a complex filter:

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt="" width="375"><figcaption><p>Complex filter specified by attribute</p></figcaption></figure>
