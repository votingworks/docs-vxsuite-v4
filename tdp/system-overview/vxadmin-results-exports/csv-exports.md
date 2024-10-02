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

# CSV Exports

Both tally reports and ballot count reports can be exported in comma-separated values (CSV) format.&#x20;

## Tally Report CSV Structure

Each row in the tally report CSV export represents a vote total for a candidate in a contest, the overvote total for a contest, or the undervote total for a contest.  For example, here is an excerpt of a tally report including the results for one contest:

```csv
Precinct,Precinct ID,Contest,Contest ID,Selection,Selection ID,Total Votes
West Lincoln,20,Mayor,mayor,Sherlock Holmes,sherlock-holmes,0
West Lincoln,20,Mayor,mayor,Thomas Edison,thomas-edison,0
West Lincoln,20,Mayor,mayor,Write-In,write-in,0
West Lincoln,20,Mayor,mayor,Overvotes,overvotes,0
West Lincoln,20,Mayor,mayor,Undervotes,undervotes,0
```

<figure><img src="../../.gitbook/assets/Screen Shot 2024-10-02 at 8.37.43 AM.png" alt=""><figcaption><p>Formatted version of the above CSV excerpt</p></figcaption></figure>

The "Precinct" and "Precinct ID" columns are [metadata fields](csv-exports.md#shared-metadata-structure) that are included because the example export  groups results by precinct. The other fields are standard fields:

<table><thead><tr><th width="162">Header</th><th>Values</th></tr></thead><tbody><tr><td>Contest</td><td>The title of the contest</td></tr><tr><td>Contest ID</td><td>The internal identifier of the contest in the election definition</td></tr><tr><td>Selection</td><td>The candidate name for candidate contests, the option label for yes-no contests, or "Overvotes" or "Undervotes"</td></tr><tr><td>Selection ID</td><td>The internal identifier of the contest option or "overvoets" or "undervotes"</td></tr><tr><td>Total Votes</td><td>The vote count for the option</td></tr><tr><td>Scanned Votes</td><td>If there are manual results included in the results, the scanned vote counts will receive their own column</td></tr><tr><td>Manual Votes</td><td>If there are manual results included in the results, the manual vote counts will receive their own column</td></tr></tbody></table>

The results of write-in adjudication are always included in the CSV exports. All write-in candidates will appear with their adjudicated name and an UUID assigned by VxAdmin. Unadjudicated write-in candidates will appear as "Unadjudicated Write-In" with the ID "write-in". Unlike in the printed reports, write-in candidates are never bucketed.&#x20;

## Ballot Count Report CSV Structure

The ballot count report CSV maps directly onto the table presented in the [printed ballot count reports](ballot-count-reports.md). For example:

```csv
Precinct,Precinct ID,Voting Method,BMD,HMPB,Total
West Lincoln,20,Precinct,0,0,0
West Lincoln,20,Absentee,0,0,0
East Lincoln,21,Precinct,0,0,0
East Lincoln,21,Absentee,0,0,0
South Lincoln,22,Precinct,0,0,0
South Lincoln,22,Absentee,0,0,0
North Lincoln,23,Precinct,0,0,0
North Lincoln,23,Absentee,0,0,0
```

<figure><img src="../../.gitbook/assets/Screen Shot 2024-10-02 at 8.52.44 AM.png" alt="" width="563"><figcaption><p>Formatted version of the above CSV excerpt</p></figcaption></figure>

The "Precinct", "Precinct ID" and "Voting Method" columns are [metadata fields](csv-exports.md#shared-metadata-structure) that are included because the example export groups results by precinct and voting method. The other fields are standard fields:

<table><thead><tr><th width="172">Header</th><th>Values</th></tr></thead><tbody><tr><td>BMD</td><td>The count of machine marked ballots</td></tr><tr><td>HMPB</td><td>The count of hand marked paper ballots. In a multi-sheet election, this is just the count of the first sheet</td></tr><tr><td>HMPB Sheet {N}</td><td>The count of a particular ballot sheet. The count of the second sheet of all ballots would be "HMPB Sheet 2"</td></tr><tr><td>Manual</td><td>The count of manually entered ballots</td></tr><tr><td>Total</td><td>The total ballot count</td></tr></tbody></table>

## Shared Metadata Structure

The CSV reports and each row within them are self-documenting in the sense that any filters or groupings which apply to each row will be indicated in the row itself, with metadata fields. If the row is filtered by a single attribute value (e.g. represents one precinct rather than multiple precincts) then the following basic metadata fields are used:

<table><thead><tr><th width="173">Header</th><th>Value</th></tr></thead><tbody><tr><td>Precinct</td><td>The name of the precinct</td></tr><tr><td>Precinct ID</td><td>The identifier of the precinct from the election definition</td></tr><tr><td>Party</td><td>The short name of the party e.g. "Republican". Included by default if the ballot style is included, in a primary</td></tr><tr><td>Party ID</td><td>The identifier of the party from the election definition</td></tr><tr><td>Ballot Style ID</td><td>The identifier of the ballot style</td></tr><tr><td>Voting Method</td><td>"Absentee", "Precinct", or "Provisional"</td></tr><tr><td>Scanner ID</td><td>The serial number of the scanner. Included by default if the batch is included</td></tr><tr><td>Batch</td><td>The label of the scanned batch</td></tr><tr><td>Batch ID</td><td>The scanner assigned UUID of the scanned batch</td></tr></tbody></table>

In cases of complex filters, the following columns may be used:

<table><thead><tr><th width="236">Header</th><th>Value</th></tr></thead><tbody><tr><td>Included Precincts</td><td>The precinct identifiers separated by commas</td></tr><tr><td>Included Parties</td><td>The party identifiers separated by commas</td></tr><tr><td>Included Ballot Styles</td><td>The ballot style identifiers separated by commas</td></tr><tr><td>Included Voting Methods</td><td>The voting method labels ("Precinct", "Absentee", or "Provisional") separated by commas</td></tr><tr><td>Included Scanners</td><td>The scanner serial numbers separated by commas</td></tr><tr><td>Included Batches</td><td>The batch identifiers separated by commas</td></tr></tbody></table>

In cases as above, where a row value includes comma-separated values, those values will be wrapped in quotation marks per typical CSV formatting in order to allow consumers to properly differentiated columns.
