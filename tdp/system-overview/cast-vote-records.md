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

## CDF Implementation

VxSuite uses the JSON [NIST Cast Vote Records CDF Specification Version 1](https://pages.nist.gov/CastVoteRecords/) as its cast vote record format. VxSuite does not use any data extensions beyond the NIST specification, but some fields are made required that are not required in the original NIST specification. The two specifications can be compared by comparing the [NIST JSON schema](https://github.com/usnistgov/CastVoteRecords/blob/master/NIST\_V0\_cast\_vote\_records.json) with the [VxSuite JSON schema](https://github.com/votingworks/vxsuite/blob/main/libs/types/src/cdf/cast-vote-records/vx-schema.json) (**insert link updated).** The additionally required fields are listed in a table below.

Because VxAdmin requires a VxSuite digital signature on all imported cast vote records, it's not possible to import a cast vote record from outside of VxSuite. The goal of using an interoperable format, like the NIST CDT, is to help external systems consume VxSuite cast vote records for audit or analysis.

### VxSuite Required Fields

These fields are required in VxSuite but not in the generic CDF specification:

<table><thead><tr><th width="219">CDF Class</th><th>Additionally Required Attributes</th></tr></thead><tbody><tr><td>CVR</td><td>BallotStyleId, BallotStyleUnitId, BatchId, CreatingDeviceId, UniqueId</td></tr><tr><td>CVRContest</td><td>CVRContestSelection</td></tr><tr><td>CVRContestSelection</td><td><ul><li>ContestSelectionId </li><li>SelectionPosition is limited to length 1</li></ul></td></tr><tr><td>CVRSnapshot</td><td>CVRContest</td></tr></tbody></table>

## Directory Structure

In order to export cast vote records efficiently and without compromising voter privacy, every cast vote record is generated individually. The structure of a cast vote record directory is as follows:

```
- root
    - 0cfaa953-11fa-4483-af03-04eed1d8cc6f // cast vote record with images
        - cast-vote-record-report.json
        - 0cfaa953-11fa-4483-af03-04eed1d8cc6f-front.jpg
        - 0cfaa953-11fa-4483-af03-04eed1d8cc6f-front.layout.json
        - 0cfaa953-11fa-4483-af03-04eed1d8cc6f-back.jpg
        - 0cfaa953-11fa-4483-af03-04eed1d8cc6f-back.layout.json
    - 864a2854-ee26-4223-8097-9633b7bed096 // cast vote record without images
        - cast-vote-record-report.json
    - rejected-0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c // rejected sheet record
        - 0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c-front.jpg
        - 0cfbf789-d8a0-4d3f-a221-b7fe8e0bb47c-back.jpg
    - ...
    - ...
    - ...
```

The cast vote record export contains a directory for each cast vote record, labelled with its UUID. Each specific cast vote record directory contains:

* **Cast Vote Record Report** - Contains information about the election and the ballot interpretation in the Common Data Format. The information in the report used as the basis for tabulation at VxAdmin.
* **Images** - Ballot images to be used in write-in adjudication or auditing
* **Interpreted Ballot Layouts -** Metadata for the position of ballot features such as contests, contest options, and bubbles in the ballot image. The interpreted layout data is used to properly crop and highlight ballot images in write-in adjudication.

### Including Ballot Images

In VxScan, ballot images and layouts are always included. In VxCentralScan, ballot images and layouts are included in the default export only if the ballot has write-ins that may require adjudication. When exporting a backup from VxCentralScan, however, ballot images and layouts are included for all ballots.

### Including Rejected Ballots

In VxScan, images of rejected ballots are always included. In VxCentralScan, images of rejected ballots are not included in the default export but are included in the backup. There are no layout files or cast vote record report for rejected ballots because they are often uninterpretable.

## CDF Cast Vote Record Report

This section describes how the various CDF attributes are used to convey information about the election and each ballot.

### Report Metadata

The CDF specification includes many metadata fields that might help a consumer make sense of the cast vote record data. For example, you may define the candidates that are referenced as contest selections. VxSuite cast vote records all include this metadata to conform to the CDF, but nearly none of it is actually utilized when imported into VxAdmin. VxAdmin already has that information from the [election package](../../system-overview/election-package/). The only data that is utilized by VxAdmin is the `GeneratedDate` and the indication of whether or not the report is a test report in `ReportType` and `OtherReportType`.

#### CastVoteRecordReport

<table><thead><tr><th width="277">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>Version</td><td>Fixed to "1.0.0"</td></tr><tr><td>ReportType</td><td>Always includes "originating-device-export". If a test report, also includes "other"</td></tr><tr><td>OtherReportType</td><td>If a test report, "test", otherwise undefined</td></tr><tr><td>GeneratedDate</td><td>Generated date in <a href="https://tc39.es/ecma262/multipage/numbers-and-dates.html#sec-date-time-string-format">Date Time String Format</a></td></tr><tr><td>ReportGeneratingDeviceIds</td><td>Contains only the scanner serial number</td></tr></tbody></table>

#### CastVoteRecordReport.ReportingDevices

Only one `ReportingDevice` is ever listed:

<table><thead><tr><th width="212">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>@id</td><td>Scanner serial number</td></tr><tr><td>SerialNumber</td><td>Scanner serial number</td></tr><tr><td>Manufacturer</td><td>Fixed to "VotingWorks"</td></tr></tbody></table>

#### CastVoteRecordReport.Party

The list of parties in the cast vote record report is mapped directly from the [Party](../../system-overview/election-package/vxsuite-election-definition.md#party-party) list in the election definition:

<table><thead><tr><th width="203">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>@id</td><td>Internal party identifier</td></tr><tr><td>Name</td><td>Full name of the party, e.g. "Democratic Party"</td></tr><tr><td>Abbreviation</td><td>Abbreviation of the party, e.g. "R"</td></tr></tbody></table>

#### CastVoteRecordReport.GpUnit

`GpUnit`s are created for each [Precinct](../../system-overview/election-package/vxsuite-election-definition.md#precinct-precinct) in the election, for the [County](../../system-overview/election-package/vxsuite-election-definition.md#county-county), and for the state:

<table><thead><tr><th width="211">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>@id</td><td><ul><li><strong>Precinct</strong>: Internal precinct identifier</li><li><strong>County</strong>: Fixed to "election-county"</li><li><strong>State:</strong> Fixed to "election-state"</li></ul></td></tr><tr><td>Type</td><td><ul><li><strong>Precinct:</strong> "precinct"</li><li><strong>County</strong> or <strong>State:</strong> "other"</li></ul></td></tr><tr><td>Name</td><td>Precinct, county, or state name</td></tr></tbody></table>

#### CastVoteRecordReport.Election

The `Election` class has values mapped to it directly from the [election definition](../../system-overview/election-package/vxsuite-election-definition.md): &#x20;

<table><thead><tr><th width="314">CDF Attribute</th><th>Usage</th></tr></thead><tbody><tr><td>@id</td><td>The election's <a href="../../system-overview/election-package/#election-package-and-ballot-hashes">ballot hash</a></td></tr><tr><td>Name</td><td>The title of the election</td></tr><tr><td>ElectionScopeId</td><td>Fixed "election-state"</td></tr><tr><td>Candidate.@id</td><td>Internal candidate identifier</td></tr><tr><td>Candidate.Name</td><td>The candidate name</td></tr><tr><td>Contest.@id</td><td>Internal contest identifier</td></tr><tr><td>Contest.Name</td><td>The contest title</td></tr><tr><td>CandidateContest.VotesAllowed</td><td>The contest's number of seats</td></tr><tr><td>CandidateContest.PrimaryPartyId</td><td>The internal identifier of the associated party, if a primary contest</td></tr><tr><td>CandidateSelection.@id</td><td>Internal candidate identifier</td></tr><tr><td>CandidateSelection.CandidateIds</td><td>Internal candidate identifier</td></tr><tr><td>CandidateSelection.IsWriteIn</td><td>Whether the selection represents a write-in bubble</td></tr><tr><td>BallotMeasureSelection.@id</td><td>Internal yes or no option identifier</td></tr><tr><td>BallotMeasureSelection.Selection</td><td>Label for the option that appeared on the ballot</td></tr></tbody></table>

### Cast Vote Record Attributes

