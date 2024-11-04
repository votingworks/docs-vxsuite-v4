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

# Write-In Adjudication Report

The write-in adjudication report includes the results of all write-in adjudication organized by contest:

<figure><img src="../../.gitbook/assets/image (11).png" alt="" width="563"><figcaption><p>Full write-in adjudication report</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt="" width="563"><figcaption><p>Write-in adjudication contest results</p></figcaption></figure>

The values in the contest table above are as follows:

<table><thead><tr><th width="245">Field</th><th>Description</th></tr></thead><tbody><tr><td>Total Write-Ins</td><td>The count of all write-ins. If unmarked write-ins are being adjudicated, they will be included in this count</td></tr><tr><td>Not Adjudicated</td><td>The count of all write-ins that have not been adjudicated in the write-in adjudication interface yet</td></tr><tr><td>Official Candidate Counts</td><td>The count of all write-ins that have been adjudicated for official candidates in the election definition</td></tr><tr><td>Write-In Candidate Counts</td><td>The count of all write-ins that have been adjudicated for write-in candidates added at VxAdmin</td></tr><tr><td>Invalid</td><td>The count of all write-ins that have been marked as invalid</td></tr></tbody></table>

## Relationship to Tally Reports

Before adjudication, write-ins are treated as votes for a generic write-in candidate and will appear in tally reports as "Unadjudicated Write-In." After adjudication, the new value will be reflected on tally reports:

* When adjudicated for an official candidate, the write-in will be added to the official candidate count just as a regular mark for the candidate would be
* When adjudicated for a write-in candidate, the write-in will appear in the adjudicated write-in bucket or are individually listed if they are[ relevant to the results](tally-reports.md#write-in-candidate-aggregation)
* When invalid, the write-in becomes an undervote

### Unmarked Write-Ins

Unmarked write-ins behave differently in relationship to the tally results because they cannot be considered a valid mark before adjudication. As a result, they are actually considered undervotes before adjudication. If the unmarked write-in is marked as invalid, then tally results are unchanged. If they're adjudicated for a candidate, the unmarked write-in is no longer an undervote and is added to the vote total for the candidate.

Also note that, because the write-in adjudication report includes unmarked write-ins, the "Unadjudicated Write-In" count on tally reports may be less than the "Not Adjudicated" count on the write-in adjudication report. The initial difference is the count of unmarked write-ins.&#x20;



