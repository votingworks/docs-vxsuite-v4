# Election Package Specification

VxAdmin is configured with an election package (see [configure-vxadmin.md](../vxadmin-system-setup/configure-vxadmin.md "mention")), which specifies the details of the election as well as various settings for the system. This page documents the format of the election package.

## Overview

An election package is a ZIP file containing a number of JSON files:

* **election.json** - The election definition (contests, ballot styles, etc.)
* **systemSettings.json** - Settings for the various machines
* **metadata.json** - Documents the election package version

There may also be a few other files present that are not used in v3.1:

* **appStrings.json, vxElectionStrings.json** - Translations of voter-facing content
* **audioClips.jsonl, audioIds.json** - Audio recordings of voter-facing content

## Election Definition (election.json)

The election definition utilizes a customized version of the NIST Ballot Definition Common Data Format (CDF), which is specified here:&#x20;

* PDF: [https://doi.org/10.6028/NIST.SP.1500-20](https://doi.org/10.6028/NIST.SP.1500-20)
* Web-friendly UML: [https://github.com/usnistgov/BallotDefinition/blob/master/BallotDefinition\_UML\_Model\_Documentation.md](https://github.com/usnistgov/BallotDefinition/blob/master/BallotDefinition\_UML\_Model\_Documentation.md)

The VotingWorks election definition format (vxCDF) modifies NIST CDF in a few ways:

* It uses only a subset of the objects and fields defined in NIST CDF
* It extends the format with some additional fields to support data that is not included in NIST CDF

For documentation of the fields used in vxCDF, refer to the schema: [https://github.com/votingworks/vxsuite/blob/v3.1.0-release-branch/libs/types/src/cdf/ballot-definition/vx-schema.json](https://github.com/votingworks/vxsuite/blob/v3.1.0-release-branch/libs/types/src/cdf/ballot-definition/vx-schema.json).

## System Settings (systemSettings.json)

The system settings uses a custom JSON format to define additional settings for the machines.

The system settings file uses the follow schema:

```json
{
  "type": "object",
  "properties": {
    "auth": {
      "type": "object",
      "properties": {
        "arePollWorkerCardPinsEnabled": { "type": "boolean" },
        "inactiveSessionTimeLimitMinutes": {
          "type": "number",
          "enum": [10, 15, 20, 30, 360]
        },
        "numIncorrectPinAttemptsAllowedBeforeCardLockout": {
          "type": "number",
          "enum": [3, 4, 5, 6, 7, 8, 9, 10]
        },
        "overallSessionTimeLimitHours": {
          "type": "number",
          "enum": [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
        },
        "startingCardLockoutDurationSeconds": {
          "type": "number",
          "enum": [15, 30, 60]
        }
```

```json
      },
      "required": [
        "arePollWorkerCardPinsEnabled",
        "inactiveSessionTimeLimitMinutes",
        "numIncorrectPinAttemptsAllowedBeforeCardLockout",
        "overallSessionTimeLimitHours",
        "startingCardLockoutDurationSeconds"
      ],
      "additionalProperties": false
      },
    "markThresholds": {
      "type": "object",
      "properties": {
        "marginal": { "type": "number", "minimum": 0, "maximum": 1 },
        "definite": { "type": "number", "minimum": 0, "maximum": 1 },
        "writeInTextArea": { "type": "number", "minimum": 0, "maximum": 1 }
      },
      "required": ["marginal", "definite"],
      "additionalProperties": false
    },
    "centralScanAdjudicationReasons": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "UninterpretableBallot",
          "MarginalMark",
          "Overvote",
          "Undervote",
          "BlankBallot",
          "UnmarkedWriteIn"
        ]
      }
    },
    "precinctScanAdjudicationReasons": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "UninterpretableBallot",
          "MarginalMark",
          "Overvote",
          "Undervote",
          "BlankBallot",
          "UnmarkedWriteIn"
        ]
      }
    },
    "precinctScanDisallowCastingOvervotes": { "type": "boolean" }
  },
  "required": [
    "auth",
    "markThresholds",
    "centralScanAdjudicationReasons",
    "precinctScanAdjudicationReasons",
    "precinctScanDisallowCastingOvervotes"
  ],
  "additionalProperties": false,
  "$schema": "http://json-schema.org/draft-07/schema#"
}
```

