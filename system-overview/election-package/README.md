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

# Election Package

The election package contains all the information which defines an election. VxAdmin is configured by selecting an election package from a mounted USB drive. After VxAdmin is configured, the election package can then be re-exported onto a USB drive and used to configure the other devices (VxScan, VxCentralScan, and VxMark).

The election package exported from VxAdmin is accompanied by a digital signature which verifies that the election package is legitimate (**insert link)**. The other devices require that the signature is present. As a result, an election package from outside the system cannot be used to directly configure VxScan, VxCentralScan, or VxMark.

## Election Package Contents

The election package is a zip archive (a `.zip` file). The zip archive contains 6 files:

* Election Definition (`election.json`)
* App Strings (`appStrings.json`)
* Audio IDs (`audioIds.json`)
* Audio Clips (`audioClips.jsonl`)
* System Settings (`systemSettings.json`)
* Metadata (`metadata.json`)

### Election Definition

The election definition file includes the information that defines the election and ballots, including but not limited to definitions for contests, ballot styles, precincts, parties, multi-lingual ballot translations, and ballot layouts. The system accepts two formats - the [VxSuite Election Definition](vxsuite-election-definition.md) format or the [Ballot Definition CDF](ballot-definition-cdf.md). When using the Ballot Definition CDF, some features are not available.&#x20;

The election definition file is strictly required within the election package. Any election package without a valid `election.json` file is an invalid election package.

### App Strings

The app strings file contains all voter-facing strings in the user interface and their translations. For example, at the beginning of the voter flow in VxMark there is a button labelled, by default, "Start Voting." If the voter has set VxMark to another language, however, the button will display the translation for that language specified in the app strings file. Additionally, the default English text can be overridden by specifying a different English value in the app strings file.

In the case of specifying a Spanish translation and overriding the English translation for "Start Voting", which has an internal key of `buttonStartVoting`, the following values and overall structure would appear in the app strings file:

```json
{
  "en": {
    ...
    "buttonStartVoting": "Begin Voting",
    ...
  },
  "es-US": {
    ...
    "buttonStartVoting": "Empezar a votar",
    ...
  }
}
```

**Notes:**

* Voter-facing strings that appear on ballots (contest names, candidate names, the name of the jurisidiction, etc.) are not included in the app strings file because they are already included in the election definition.
* The language codes in the app strings file are the [IETF language tags](https://www.w3.org/International/articles/language-tags/) for supported VxSuite languages: English, Spanish, Simplified Chinese, and Traditional Chinese.
* The keys for the various user interface app strings (e.g. `buttonStartVoting`) are defined in VxSuite's app string catalog (**insert link**)

### Audio IDs & Audio Clips

The audio IDs file is a JSON file structured identically to the app strings file except that, instead of containing text values for each voter string, it contains audio IDs for each voter string. Each audio ID corresponds to an entry in the audio clips file.&#x20;

```json
{
  "en": {
    ...
    "buttonStartVoting": "AUDIO_ID_1",
    ...
  },
  "es-US": {
    ...
    "buttonStartVoting": "AUDIO_ID_2",
    ...
  }
}
```

Each row of the audio clips file contains one audio clip with relevant metadata. The audio itself appears as an MP3 file encoded in base 64. For example, a row representing an audio clip for the "Start Voting" button would appear as:

```json
{ "languageCode": "en", "id": "AUDIO_ID_1", "dataBase64": "YnV0dG9uU3..." }
{ "languageCode": "es-US", "id": "AUDIO_ID_2", "dataBase64": "DnX0eG6uY3..." }
...
```

Together, the two files allow specifying audio playback for any text read to a voter in audio mode, including both non-English translations and English overrides.

### System Settings

The system settings file contains settings which are not specific to an election definition but do impact machine behavior.

```json
{
  "auth": {
    "arePollWorkerCardPinsEnabled": false,
    "inactiveSessionTimeLimitMinutes": 30,
    "numIncorrectPinAttemptsAllowedBeforeCardLockout": 5,
    "overallSessionTimeLimitHours": 12,
    "startingCardLockoutDurationSeconds": 15
  },
  "markThresholds": {
    "marginal": 0.05,
    "definite": 0.07,
    "writeInTextArea": 0.05
  },
  "centralScanAdjudicationReasons": [],
  "precinctScanAdjudicationReasons": [],
  "precinctScanDisallowCastingOvervotes": false
}
```

* Authentication Settings
  * `arePollWorkerCardPinsEnabled` - When set to `true`, poll worker cards are created with PINs which are then required when authenticating.
  * `inactiveSessionTimeLimitMinutes`- Sets the number of minutes after which machines automatically lock due to inactivity.
  * `numIncorrectPinAttemptsAllowedBeforeCardLockout`- Sets the number of times that a PIN can be entered incorrectly before the user has to wait extra time to retry.
  * `overallSessionTimeLimitHours`- Sets the maximum number of hours for any session, regardless of activity.
  * `startingCardLockoutDurationSeconds` - Sets the number of seconds that the user is locked out from retrying a PIN after the number of failed attempts specified by  `numIncorrectPinAttemptsAllowedBeforeCardLockout`. Each subsequent failed attempt triggers a lockout double the length of the previous lockout.
* Scanning Thresholds
  * `definite` - Specifies the percentage of a bubble that needs to be filled in for the tabulators to consider it a mark.
  * `marginal` - Specifies the percentage of a bubble that needs to be filled in for the tabulators to consider it a marginal mark.
  * `writeInTextArea` - Specifies the percentage of the write-in area that needs to be filled in for the tabulators to consider it a write-in. This is only relevant for jurisdictions that allow unmarked write-ins i.e write-ins without an accompanying mark.
* Adjudication Reasons
  * `precinctScanAdjudicationReasons` - Specifies the reasons that a ballot should be labelled as needing later adjudication at VxScan. Supported reasons are overvotes, undervotes, blank ballots, or unmarked write-ins.&#x20;
  * `centralScanAdjudicationReasons` - Specifies the reasons that a ballot should be labelled as needing later adjudication at VxCentral. Supported reasons are overvotes, undervotes, blank ballots, or unmarked write-ins.&#x20;
  * `precinctScanDisallowCastingOvervotes` - When set to `false`, an overvoted ballot on VxScan will trigger an onscreen prompt from which the voter has the option to cast their ballot with the overvote. When set to `true`, overvoted ballots are always rejected and cannot be cast.

### Metadata

The metadata file is a JSON file that contains a single key, `version`. In the current software version, the value will only ever be `"latest"`. In other words, the metadata file is a JSON file with the contents:

```json
{
  "version": "latest"
}
```

In future software versions, the `"version"` value will be used to differentiate versions of the election package that correspond to different software versions. For example, if a user flow is updated, a new app string may be added and the `"version"` value will indicate which app strings to expect.

## Election Package and Ballot Hashes

There are two hashes for each election which are both critical to operation and security of each election.

The **ballot hash** is the SHA256 hash of the election definition file and represents a snapshot of all election-specific data which determines the ballot, including contest definitions and ballot layout. Ballots must include the ballot hash in some form, whether encoded into a QR code or into timing marks such that, when scanned, it's possible to confirm they have the correct ballot hash. If the ballot hash changes for an election, it is considered by the system to be a new election, and any ballots with a different ballot hash will not scan. The system's strict adherence to the ballot hash prevents situations where a change to the ballot definition leads to ballots being miscounted (for example, if the order of two candidates is swapped). The consequence is that changes to the election definition require reprinting all ballots.&#x20;

The **election package hash** is the SHA256 hash of the entire election package, which includes the election definition but also all other files. The election package is displayed on screen to election managers and system administrators across applications. It allows the user, at a glance, to ascertain the current configuration of a machine.

For example, imagine that an election administrator wants to change the audio clip for candidate's name. The audio clip is not a part of the election definition but it is a part of the election package, so the ballot hash remains the same while the election package hash changes. The election administrator can reconfigure VxMark with an updated election package but does not have to reprint ballots.

