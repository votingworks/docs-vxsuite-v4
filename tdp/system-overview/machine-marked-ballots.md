# Machine Marked Ballots

After a voter is done making selections at VxMark, the machine will print a ballot representing the selections. The voter reviews the ballot, after which it is deposited in the attached ballot box. Eventually, those ballots are scanned at VxScan or VxCentralScan.

<figure><img src="../.gitbook/assets/image (14).png" alt="" width="563"><figcaption><p>VxMark ballot</p></figcaption></figure>

## Ballot Layout

<figure><img src="../.gitbook/assets/image (15).png" alt="" width="563"><figcaption><p>Parts of a VxMark ballot</p></figcaption></figure>

The ballot displays information about the election, metadata about the ballot, and the voter's selections. The selections are both displayed and encoded in the QR code.&#x20;

<table><thead><tr><th width="232">Ballot Component</th><th>Details</th></tr></thead><tbody><tr><td>Election Seal</td><td>The seal included in the election definition</td></tr><tr><td>Ballot Title</td><td>The title is either "Unofficial Test Ballot" or "Official Ballot" depending whether VxMark is in test mode</td></tr><tr><td>Election Metadata</td><td>Includes the election title, election date, state, and county</td></tr><tr><td>Ballot Metadata</td><td>Includes the precinct name, the ballot style identifier, and the ballot identifier. The ballot identifier is a random UUID assigned by VxMark</td></tr><tr><td>QR Code</td><td>See <a href="machine-marked-ballots.md#qr-code">QR Code</a></td></tr><tr><td>Contest Title</td><td>The contest title name</td></tr><tr><td>Selection</td><td>The name of the candidate or label of the yes-no contest option</td></tr><tr><td>Party</td><td>The short party name specified</td></tr></tbody></table>

The padding at the top of the ballot is included so the entire ballot is visible when presenting the ballot to the voter at VxMark.

### Multi-Lingual Ballots

If VxMark is being used in a language other than English, the resulting ballot will be multi-lingual and feature the other language. All pieces of text that appear on the VxMark ballot may have translations specified in the [ballot strings](election-package/vxsuite-election-definition.md#ballot-strings) specified in the election definition which will then be used when printing the ballot.

<figure><img src="../.gitbook/assets/image (16).png" alt="" width="563"><figcaption><p>English/Chinese VxMark ballot</p></figcaption></figure>

## QR Code

The QR codes on VxMark ballots are different than the [QR codes on hand marked ballots](hand-marked-ballots.md#qr-code-metadata) in that they actually contain voter selections rather than purely metadata. For full specifications on how metadata and selections are encoded, view the [ballot encoder documentation](https://github.com/votingworks/vxsuite/tree/main/libs/ballot-encoder#hmpb-metadata-encoding) (**insert link updated)**.
