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

# Cast Vote Records

A cast vote records is a record of voter selections based on the system's interpretation of a scanned ballot. Each cast vote record corresponds to a single scanned ballot sheet, which means that multi-sheet ballots correspond to multiple cast vote records.

Cast vote records are exported from VxScan and VxCentralScan onto USB drives and then imported into VxAdmin. Each cast vote record export is created with a digital signature which must be valid in order to successfully import it into VxAdmin. A valid signature ensures that the files have not been tampered with.

## Directory Structure

In order to export cast vote records efficiently and without compromising voter privacy, every cast vote record is generated individually. The structure of a cast vote record directory is as follows:

```
- root
    - metadata.json
    - 0cfaa953-11fa-4483-af03-04eed1d8cc6f
        - cast-vote-record-report.json
        - 0cfaa953-11fa-4483-af03-04eed1d8cc6f-front.jpg
        - 0cfaa953-11fa-4483-af03-04eed1d8cc6f-front.layout.json
        - 0cfaa953-11fa-4483-af03-04eed1d8cc6f-back.jpg
        - 0cfaa953-11fa-4483-af03-04eed1d8cc6f-back.layout.json
    - 0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c
        - cast-vote-record-report.json 
        - 0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c-front.jpg
        - 0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c-front.layout.json
        - 0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c-back.jpg
        - 0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c-back.layout.json
    - ...
    - ...
    - ...
```

The cast vote record export contains a directory for each cast vote record, labelled with its UUID. Each specific cast vote record directory contains:

* **Cast Vote Record Report** - Contains information about the election and the ballot interpretation in the Common Data Format. The information in the report used as the basis for tabulation at VxAdmin.
* **Images** - Ballot images to be used in write-in adjudication or auditing
* **Interpreted Ballot Layouts -** Metadata for the position of ballot features such as contests, contest options, and bubbles in the ballot image. The interpreted layout data is used to properly crop and highlight ballot images in write-in adjudication.

In addition, there is a metadata file that applies to the entire export at the root of the directory, **metadata.json.**

### Including Ballot Images

In VxScan, ballot images and layouts are always included. In VxCentralScan, ballot images and layouts are included in the default export only if the ballot has write-ins that may require adjudication. When exporting a backup from VxCentralScan, however, ballot images and layouts are included for all ballots.

Layouts are not included for machine marked ballots.

### Including Rejected Ballots

In VxScan, images of rejected ballots are always included. In VxCentralScan, images of rejected ballots are not included in the default export but are included in the backup. There are no layout files or cast vote record report for rejected ballots because they are often uninterpretable. When rejected ballots are included, they will appear in the directory as in the following example:

```
- root
    - ...
    - rejected-0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c
        - 0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c-front.jpg
        - 0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c-back.jpg
    - ...
```

## Cast Vote Record Report

### CDF Implementation

VxSuite does not use any data extensions beyond the NIST specification, but some fields are made required that are not required in the original NIST specification. The two specifications can be compared by comparing the [NIST JSON schema](https://github.com/usnistgov/CastVoteRecords/blob/master/NIST\_V0\_cast\_vote\_records.json) with the [VxSuite JSON schema](https://github.com/votingworks/vxsuite/blob/main/libs/types/src/cdf/cast-vote-records/vx-schema.json) (**insert link updated).** The additionally required fields are listed in a table below.

Because VxAdmin requires a VxSuite digital signature on all imported cast vote records, it's not possible to import a cast vote record from outside of VxSuite. The goal of using an interoperable format, like the NIST CDT, is to help external systems consume VxSuite cast vote records for audit or analysis.

#### VxSuite Required Fields

<table><thead><tr><th width="219">CDF Class</th><th>Additionally Required Attributes</th></tr></thead><tbody><tr><td>CVR</td><td>BallotStyleId, BallotStyleUnitId, BatchId, CreatingDeviceId, UniqueId</td></tr><tr><td>CVRContest</td><td>CVRContestSelection</td></tr><tr><td>CVRContestSelection</td><td><ul><li>ContestSelectionId </li><li>SelectionPosition is limited to length 1</li></ul></td></tr><tr><td>CVRSnapshot</td><td>CVRContest</td></tr></tbody></table>

### Report Metadata

The CDF specification includes many metadata fields that might help a consumer make sense of the cast vote record data. For example, you may define the candidates that are referenced as contest selections. VxSuite cast vote records all include this metadata to conform to the CDF, but nearly none of it is actually utilized when imported into VxAdmin. VxAdmin already has that information from the [election package](election-package/). The only data that is utilized by VxAdmin is the `GeneratedDate` and the indication of whether or not the report is a test report in `ReportType` and `OtherReportType`.

#### CastVoteRecordReport

<table><thead><tr><th width="277">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>Version</td><td>Fixed to "1.0.0"</td></tr><tr><td>ReportType</td><td>Always includes "originating-device-export". If a test report, also includes "other"</td></tr><tr><td>OtherReportType</td><td>If a test report, "test", otherwise undefined</td></tr><tr><td>GeneratedDate</td><td>The generated date in <a href="https://tc39.es/ecma262/multipage/numbers-and-dates.html#sec-date-time-string-format">Date Time String Format</a></td></tr><tr><td>ReportGeneratingDeviceIds</td><td>The scanner serial number</td></tr></tbody></table>

#### CastVoteRecordReport.ReportingDevices

Only one `ReportingDevice` is ever listed:

<table><thead><tr><th width="212">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>@id</td><td>The scanner serial number</td></tr><tr><td>SerialNumber</td><td>The scanner serial number</td></tr><tr><td>Manufacturer</td><td>Fixed to "VotingWorks"</td></tr></tbody></table>

#### CastVoteRecordReport.Party

The list of parties in the cast vote record report is mapped directly from the [Party](election-package/vxsuite-election-definition.md#party-party) list in the election definition:

<table><thead><tr><th width="203">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>@id</td><td>The party identifier from the election definition</td></tr><tr><td>Name</td><td>The full name of the party, e.g. "Democratic Party"</td></tr><tr><td>Abbreviation</td><td>The abbreviation of the party, e.g. "R"</td></tr></tbody></table>

#### CastVoteRecordReport.GpUnit

`GpUnit`s are created for each [Precinct](election-package/vxsuite-election-definition.md#precinct-precinct) in the election, for the [County](election-package/vxsuite-election-definition.md#county-county), and for the state:

<table><thead><tr><th width="211">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>@id</td><td><ul><li><strong>Precinct</strong>: The precinct identifier from the election definition</li><li><strong>County</strong>: Fixed to "election-county"</li><li><strong>State:</strong> Fixed to "election-state"</li></ul></td></tr><tr><td>Type</td><td><ul><li><strong>Precinct:</strong> "precinct"</li><li><strong>County</strong> or <strong>State:</strong> "other"</li></ul></td></tr><tr><td>Name</td><td>The precinct, county, or state name</td></tr></tbody></table>

#### CastVoteRecordReport.Election

The `Election` class has values mapped to it directly from the [election definition](election-package/vxsuite-election-definition.md): &#x20;

<table><thead><tr><th width="314">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>@id</td><td>The election's <a href="election-package/#election-package-and-ballot-hashes">ballot hash</a></td></tr><tr><td>Name</td><td>The title of the election</td></tr><tr><td>ElectionScopeId</td><td>Fixed to "election-state"</td></tr><tr><td>Candidate.@id</td><td>The candidate identifier from the election definition</td></tr><tr><td>Candidate.Name</td><td>The candidate name</td></tr><tr><td>Contest.@id</td><td>The contest identifier from the election definition</td></tr><tr><td>Contest.Name</td><td>The contest title</td></tr><tr><td>CandidateContest.VotesAllowed</td><td>The contest's number of seats</td></tr><tr><td>CandidateContest.PrimaryPartyId</td><td>The party identifier of the associated party, if a primary contest</td></tr><tr><td>CandidateSelection.@id</td><td>The candidate identifier from the election definition</td></tr><tr><td>CandidateSelection.CandidateIds</td><td>The candidate identifier from the election definition</td></tr><tr><td>CandidateSelection.IsWriteIn</td><td>Whether the selection represents a write-in bubble</td></tr><tr><td>BallotMeasureSelection.@id</td><td>The option identifier  from the election definition</td></tr><tr><td>BallotMeasureSelection.Selection</td><td>The option label that appeared on the ballot</td></tr></tbody></table>

### Cast Vote Record Attributes

Each cast vote record includes a set of ballot metadata attributes:

<table><thead><tr><th width="267">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>BallotSheetId</td><td>The index of the sheet within the ballot. For the second sheet of a multi-sheet ballot, it would be 2</td></tr><tr><td>BallotStyleId</td><td>The ballot style identifier from the election definition</td></tr><tr><td>BallotStyleUnitId</td><td>The precinct identifier from the election definition</td></tr><tr><td>Batch</td><td>The batch identifier</td></tr><tr><td>CreatingDeviceId</td><td>The scanner serial number</td></tr><tr><td>ElectionId</td><td>The election's <a href="election-package/#election-package-and-ballot-hashes">ballot hash</a></td></tr><tr><td>PartyIds</td><td>The party identifier from the election definition, if for a primary ballot</td></tr><tr><td>UniqueId</td><td>The UUID for the ballot generated by the scanner</td></tr><tr><td>BatchSequenceId</td><td>When using VxCentralScan, contains the index of the sheet within the batch. 1-indexed.</td></tr><tr><td>BallotAuditId</td><td>When using an imprinter on VxCentralScan, contains the UUID imprinted on the ballot</td></tr></tbody></table>

#### Ballot Images

The `CVR.BallotImage` attribute exists when there are images accompanying the cast vote record. If it exists, it always contains images for both sides of the ballot. Its attributes are as follows:

<table><thead><tr><th width="165">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>Location</td><td><p>Location of the image file relative to the report, such as:</p><pre><code>file:864a2854-ee26-4223-8097-9633b7bed096-front.jpg
</code></pre></td></tr><tr><td>Hash.Type</td><td>Fixed to "sha-256"</td></tr><tr><td>Hash.Value</td><td><ul><li><strong>No Images:</strong> Undefined</li><li><strong>Images &#x26; Layouts:</strong> {SHA256 hash of image}-{SHA256 hash of layout}</li><li><strong>Images Only</strong>: SHA256 hash of image</li></ul><p></p></td></tr></tbody></table>

Hashes of the ballot image and ballot layout files are included in the cast vote record report so that the hash (and digital signature) of the cast vote record export will reflect any change to the image or layout files.

#### Snapshots

The CDF specification allows detailing multiple versions of the same cast vote record as "snapshots."&#x20;

For hand marked paper ballots, there are both "original" and "modified" snapshots. The "original" snapshot contains mark thresholds for every single bubble on the ballot and is included purely for auditability. The "modified" snapshot contains only the marks that were detected as definite marks and counted as valid or invalid votes.&#x20;

For machine marked ballots, there is only an "original" snapshot.

The snapshot is referenced in the `CVR.CurrentSnapshotId` field by it's identifier, which will be the unique identifier of the cast vote record along with its type, such as&#x20;

```
864a2854-ee26-4223-8097-9633b7bed096-modified
```

#### Ballot Type

The CDF specification does not have any allowance for a ballot type such as "absentee" or "precinct" at the metadata level, so it is added as information to each snapshot:

<table><thead><tr><th width="285">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>CVRSnapshot.Status</td><td>Fixed to <code>["other"]</code></td></tr><tr><td>CVRSnapshot.OtherStatus</td><td><p>JSON blob representing the ballot type. The possible values are "absentee", "precinct", or "provisional".</p><pre class="language-json"><code class="lang-json">{
  ballotType: "absentee"
}
</code></pre></td></tr></tbody></table>

### Representing Votes

The `CVRContest` class within each snapshot contains a list of vote records by contest. The fields are used as follows:

<table><thead><tr><th width="351">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>CVRContest.ContestId</td><td>The contest identifier from the election definition</td></tr><tr><td>CVRContest.Overvotes</td><td>The number of overvotes for a contest. The number can only be 0 or the maximum number of votes in the contest</td></tr><tr><td>CVRContest.Undervotes</td><td>The number of undervotes for a contest</td></tr><tr><td>CVRContest.Status</td><td><p>The list of applicable contest statuses:</p><ul><li>"not-indicated" - no votes cast in contest</li><li>"undervoted" - fewer than allowed votes cast in contest</li><li>"overvoted" - more than allowed votes cast in contest</li><li>"invalidated-rules" - applies if overvoted</li></ul></td></tr><tr><td>CVRContestSelection.ContestSelectionId</td><td>The option identifier from the election definition</td></tr><tr><td>CVRContestSelection.OptionPosition</td><td>The index of the contest position within the contest</td></tr><tr><td>CVRContestSelection.Status</td><td><p>The list of applicable contest selection statuses:</p><ul><li>"invalidated-rules" - mark is part of an overvote</li><li>"needs-adjudication" - mark corresponds to a write-in</li></ul></td></tr><tr><td>SelectionPosition.HasIndication</td><td>"yes" or "no" depending on whether a mark in the bubble passed the mark threshold. In the original hand marked paper ballot snapshots, this may be either value. In the modified snapshot, it is always "yes" except for unmarked write-ins</td></tr><tr><td>SelectionPosition.NumberVotes</td><td>Fixed to 1</td></tr><tr><td>SelectionPosition.IsAllocable</td><td><p>"yes" except:</p><ul><li>"no" if an overvote</li><li>"unknown" if an unmarked write-in</li></ul></td></tr><tr><td>SelectionPosition.MarkMetricValue</td><td>The mark score, a decimal between 0 and 1.00 such as 0.23. Only included in the original snapshots.</td></tr><tr><td>SelectionPosition.Status</td><td><ul><li>"invalidated-rules" if an overvote</li><li>"needs-adjudication" if an unmarked write-in</li></ul></td></tr><tr><td>SelectionPosition.OtherStatus</td><td>"unmarked-write-in" if an unmarked write-in</td></tr><tr><td>CVRWriteIn.WriteInImage</td><td>The <code>BallotImage</code> data for the side of the sheet on which the write-in occurs</td></tr></tbody></table>

## Ballot Images

Ballot images are `.jpg` files are included in the cast vote record to be used for write-in adjudication or auditing. They are the image generated by the scanner, normalized to reduce skew and enforce a consistent orientation. Images from VxCentralScan are in grayscale while images for VxScan are in black and white.

## Ballot Layouts

Ballot layouts are JSON files which describe the geometry of the interpreted ballots including where each contest and contest option appears. Although the layout of each ballot is in the election definition, each scanned image may have slightly different positioning due to offset or skew of the ballot. As a result, the layouts are included in order to have accurate image highlights and crops for write-in adjudication.

## Export Metadata

The metadata file includes data that applies to all cast vote records in the export. There is only one per export. The relevant attributes are:

<table><thead><tr><th width="301">Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>arePollsClosed</td><td>For VxScan exports, the flag indicates whether polls where closed at the time of export. If polls were not closed, that may indicate an incomplete export</td></tr><tr><td>castVoteRecordReportMetadata</td><td>The <a href="cast-vote-records.md#cast-vote-record-report">cast vote record report</a> without any specific cast vote record data. In other words, only data about the election and its contests</td></tr><tr><td>castVoteRecordRootHash</td><td>A hash of all cast vote record files in the export. Including the hash here, which rolls up into the digital signature, ensures that cast vote records cannot be added or removed from the export</td></tr><tr><td>batchManifest</td><td>The list of batches on the originating scanner, see below</td></tr></tbody></table>

### Batch Manifest

Each cast vote record is associated with a batch via its `BatchId` metadata field. The CDF doesn't have a place within the cast vote record report to include batch metadata, so it is included here.

<table><thead><tr><th width="231">Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>id</td><td>The UUID of the batch generated by the scanner</td></tr><tr><td>label</td><td>The label for the batch</td></tr><tr><td>batchNumber</td><td>The sequential number of the batch, e.g. 2 for the second batch</td></tr><tr><td>startTime</td><td>The time a batch was started in ISO 8601 format</td></tr><tr><td>endTime</td><td>The time a batch ended in ISO 8601 format</td></tr><tr><td>sheetCount</td><td>The number of sheets (i.e. cast vote records) in a batch</td></tr><tr><td>scannerId</td><td>The serial number of the scanner</td></tr></tbody></table>

