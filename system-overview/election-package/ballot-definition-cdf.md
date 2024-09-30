# Ballot Definition CDF

The election definition within the election package can be a JSON Ballot Definition CDF Version 1.0 file. The full specification is defined by NIST and can be [accessed on their website](https://www.nist.gov/publications/ballot-definition-common-data-format-specification).&#x20;

## VxSuite CDF Implementation

VxSuite accepts the Ballot Definition CDF Version 1.0 as defined by NIST without any data extensions. VxSuite requirements differ from the NIST CDF schema only in the following respects:

* Some fields not required in the NIST CDF but are required in VxSuite
* Some enumeration values are more restricted in VxSuite than in the NIST CDF
* Some classes and attributes are ignored in VxSuite

The exact VxSuite schema is defined as a [JSON schema in the vxsuite repository](https://github.com/votingworks/vxsuite/blob/main/libs/types/src/cdf/ballot-definition/vx-schema.json) (**insert link updated)** which is derived from the [original NIST schema](https://github.com/usnistgov/BallotDefinition/blob/master/NIST\_V1\_ballot\_definition.json). The differences between the two are documented in the below tables.

### Required Class Attributes

<table><thead><tr><th width="224">CDF Class</th><th>VxSuite Attribute Requirements</th></tr></thead><tbody><tr><td>BallotDefinition</td><td><ul><li>BallotFormat, Election, GpUnit, and Party are required</li><li>BallotFormat and Election must have a length of 1</li><li>GpUnit must have a minimum of length 1</li></ul></td></tr><tr><td>BallotMeasureContest</td><td><ul><li>BallotTitle, ContestOption, and FullText are required</li><li>ContestOption must have a length of 2</li></ul></td></tr><tr><td>BallotStyle</td><td><ul><li>ExternalIdentifier is required and must have a length of 1</li><li>Language must have a minimum length of 1</li></ul></td></tr><tr><td>CandidateContest</td><td><ul><li>BallotTitle and ContestOption are required</li><li>ContestOption must have a minimum of length 1</li><li>PrimaryPartyIds must have a length of 1 if it exists</li></ul></td></tr><tr><td>CandidateOption</td><td>CandidateIds must have a length of 1</td></tr><tr><td>Election</td><td>BallotStyle, Contest, and ExternalIdentifier are required and all must have a minimum length of 1</td></tr><tr><td>GpUnit</td><td><ul><li>At least one GpUnit must be defined with the type "state"</li><li>At least one GpUnit must be defined with the type "county"</li></ul></td></tr><tr><td>Office</td><td>Term is required</td></tr><tr><td>OptionPosition</td><td>Sheet is required</td></tr><tr><td>OrderedContest</td><td>Physical is required and must have a minimum length of 1</td></tr><tr><td>Party</td><td>Abbreviation is required</td></tr><tr><td>PhysicalContest</td><td>PhysicalContestOption is required and must have a minimum length of 1</td></tr><tr><td>PhysicalContestOption</td><td>ContestOptionId is required</td></tr><tr><td>ReportingUnit</td><td>Name is required</td></tr><tr><td>Term</td><td>Label is required</td></tr></tbody></table>

### Restricted Enums

<table><thead><tr><th width="196">CDF Enum</th><th>Allowed Values</th></tr></thead><tbody><tr><td>ElectionType</td><td>general, primary</td></tr><tr><td>ReportingUnitType</td><td>county, precinct, split-precinct, state, other</td></tr></tbody></table>

### Ignored Classes and Enums

| CDF Entity                 |
| -------------------------- |
| ActivationContest          |
| ActivationOption           |
| AnnotatedString            |
| AnnotatedUri               |
| BallotMeasureType          |
| CandidatePreElectionStatus |
| Coalition                  |
| ContactInformation         |
| DayType                    |
| ElectionAdministration     |
| GeoSpatialFormat           |
| Hours                      |
| LatLng                     |
| OfficeGroup                |
| OfficeTermType             |
| OrderedHeader              |
| PartyContest               |
| PartyOption                |
| PartyPreferenceContest     |
| PartyRegistration          |
| Person                     |
| RetentionContest           |
| Schedule                   |
| ShortString                |
| SpatialDimension           |
| SpatialExtent              |
| StraightPartyContest       |
| StraightPartyRuleset       |
| TimeWithZone               |
| VoteVariation              |

### Ignored Class Attributes

<table><thead><tr><th width="224">CDF Class</th><th>Ignored Attributes</th></tr></thead><tbody><tr><td>BallotDefinition</td><td>IsTest, Notes, OfficeGroup, Person, TestType</td></tr><tr><td>BallotMeasureContest</td><td>Abbreviation, BallotSubTitle, ContStatement, EffectOfAbstain, ExternalIdentifier, HasRotation, InfoUri, OtherType, OtherVoteVariation, PassageThreshold, ProStatement, SequenceOrder, SummaryText, TotalSubUnits, Type, VoteVariation</td></tr><tr><td>BallotMeasureOption</td><td>ExternalIdentifier, SequenceOrder</td></tr><tr><td>BallotStyle</td><td>ImageUri, Purpose</td></tr><tr><td>Candidate</td><td>CampaignSlogan, ContactInformation, ExternalIdentifier, FileDate, IsIncumbent, IsTopTicket, PartyId, PersonId, PreElectionStatus, ReadName</td></tr><tr><td>CandidateContest</td><td>Abbreviation, BallotSubTitle, ExternalIdentifier, HasRotation, NumberElected, NumberRunoff, OtherVoteVariation, RanksAllowed, SequenceOrder, TotalSubUnits, VoteVariation</td></tr><tr><td>CandidateOption</td><td>ExternalIdentifier, SequenceOrder</td></tr><tr><td>Election</td><td>ContactInformation, OtherType</td></tr><tr><td>Office</td><td>ContactInformation, Description, ElectionDistrictId, ExternalIdentifier, FilingDeadline, IsPartisan, OfficeHolderPersonIds</td></tr><tr><td>OrderedContest</td><td>OrderedContestOptionIds</td></tr><tr><td>Party</td><td>Color, ContactInformation, ExternalIdentifier, IsRecognizedParty, LeaderPersonIds, LogoUri, PartyScopeGpUnitIds, Slogan</td></tr><tr><td>ReportingUnit</td><td>AuthorityIds, ContactInformation, ElectionAdministration, ExternalIdentifier, IsDistricted, IsMailOnly, Number, OtherType, PartyRegistration, SpatialDimension, TotalSubUnits, VotersRegistered</td></tr><tr><td>Term</td><td>EndDate, StartDate, Type</td></tr></tbody></table>



## VxSuite CDF Conversion

When importing a Ballot Definition CDF file, attributes will be mapped to the [VxSuite Election Definition](vxsuite-election-definition.md)  and used across the system in the exact same way.&#x20;

### Attribute Mappings

<table><thead><tr><th width="375">Ballot Definition CDF Attribute</th><th>VxSuite Election Definition Attribute</th></tr></thead><tbody><tr><td>Election.ExternalIdentifier</td><td>Election.id</td></tr><tr><td>Election.Type</td><td>Election.type</td></tr><tr><td>Election.Name</td><td>Election.title</td></tr><tr><td>Election.StartDate</td><td>Election.date</td></tr><tr><td>GpUnit.id</td><td>County.id, Precinct.id, District.id</td></tr><tr><td>GpUnit.Name</td><td>Election.state, County.name, Precinct.name, District.name</td></tr><tr><td>Party.id</td><td>Party.id</td></tr><tr><td>Party.Name</td><td>Party.name</td></tr><tr><td>Party.Name</td><td>Party.fullName</td></tr><tr><td>Party.Abbreviation</td><td>Party.abbrev</td></tr><tr><td>Contest.id</td><td>Contest.id</td></tr><tr><td>Contest.BallotTitle</td><td>Contest.title</td></tr><tr><td>Contest.ElectionDistrictId</td><td>Contest.districtId</td></tr><tr><td>CandidateContest.VotesAllowed</td><td>CandidateContest.seats</td></tr><tr><td>CandidateContest.ContestOption.IsWriteIn</td><td>CandidateContest.allowWriteIns</td></tr><tr><td>CandidateContest.PrimaryPartyIds</td><td>CandidateContest.partyId</td></tr><tr><td>Office.Term.Label</td><td>CandidateContest.termDescription</td></tr><tr><td>Candidate.id</td><td>Candidate.id</td></tr><tr><td>Candidate.BallotName</td><td>Candidate.name</td></tr><tr><td>CandidateOption.EndorsementPartyIds</td><td>Candidate.partyIds</td></tr><tr><td>BallotMeasureContest.FullText</td><td>YesNoContest.description</td></tr><tr><td>BallotMeasureContestOption.id</td><td>YesNoContestOption.id</td></tr><tr><td>BallotMeasureContestOption.Selection</td><td>YesNoContestOption.label</td></tr><tr><td>BallotStyle.ExternalIdentifier.Value</td><td>BallotStyle.id</td></tr><tr><td>BallotStyle.GpUnitIds</td><td>BallotStyle.districts, BallotStyle.precincts</td></tr><tr><td>BallotStyle.PartyIds</td><td>BallotStyle.partyId</td></tr><tr><td>BallotStyle.Language</td><td>BallotStyle.languages</td></tr><tr><td>BallotFormat.ShortEdge</td><td>BallotLayout.width</td></tr><tr><td>BallotFormat.LongEdge</td><td>BallotLayout.height</td></tr><tr><td>OrderedContest.ContestId</td><td>GridPosition.contestId</td></tr><tr><td>PhysicalContestOption.OptionPosition.Sheet</td><td>GridPosition.sheet</td></tr><tr><td>PhysicalContestOption.OptionPosition.Side</td><td>GridPosition.side</td></tr><tr><td>PhysicalContestOption.OptionPosition.X</td><td>GridPosition.column</td></tr><tr><td>PhysicalContestOption.OptionPosition.Y</td><td>GridPosition.row</td></tr><tr><td>PhysicalContestOption.ContestOptionId</td><td>GridPositionOption.optionId</td></tr><tr><td>PhysicalContestOption.ContestOptionId</td><td>GridPositionWriteIn.writeInIndex</td></tr><tr><td>PhysicalContestOption.WriteInPosition.X</td><td>GridPositionWriteIn.writeInArea.x</td></tr><tr><td>PhysicalContestOption.WriteInPosition.Y</td><td>GridPositionWriteIn.writeInArea.y</td></tr><tr><td>PhysicalContestOption.WriteInPosition.W</td><td>GridPositionWriteIn.writeInArea.width</td></tr><tr><td>PhysicalContestOption.WriteInPosition.H</td><td>GridPositionWriteIn.writeInArea.height</td></tr></tbody></table>

### Translations

Most attributes in the Ballot Definition CDF that could require translation are defined with the CDF `InternationalizedText` class which allows specifying variants for each language. InternationalizedText maps directly onto VxSuite's [ballot strings](vxsuite-election-definition.md#ballot-strings). When an `InternationalizedText` attribute is mapped to a ballot string, the English version is used as the default which will appear on reports and administrator interfaces while the translations are maintained in the election definition for multi-language experiences on voter devices.

### Geographies

The Ballot Definition defines all geographies as `GpUnit`s, whereas the VxSuite Election Definition defines various geographies.

Some geographies _must_ exist in the Ballot Definition CDF file to be used in VxSuite. There must be one `GpUnit` of type `state` and one of type `county` to populate the relevant metadata on the [Election](vxsuite-election-definition.md#election-election).

Any `GpUnit` of type `precinct` is mapped to a [Precinct](vxsuite-election-definition.md#precinct-precinct).

Any `GpUnit` with an associated contest is mapped to a [District](vxsuite-election-definition.md#district-district).

## VxSuite CDF Limitations

Because VxSuite does not utilize any data extensions to the Ballot Definition CDF, some information cannot be included when using the Ballot Definition CDF. The missing information corresponds to some limitations when using the Ballot Definition CDF when compared to the [VxSuite Election Definition](vxsuite-election-definition.md) format:

* Contest term descriptions (e.g. “2 years”) will always show up in English because there is no field in the CDF for internationalized term descriptions
* The full party name will be displayed for each candidate on VxMark (e.g. “Democratic Party” instead of “Democrat”) because the CDF only has one attribute for party name. In contrast, the VxSuite format supports two separate fields, one for the full name and one for showing on the ballot.
* When adjudicating write-ins, the crop area will be set to a default because there is no field in the CDF for this parameter.
* Seal images are not supported in the CDF, so no seal will be shown in association with the election.
