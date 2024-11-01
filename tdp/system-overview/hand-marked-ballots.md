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

# Hand Marked Ballots

VxSuite can accept an enormous range of ballots, which can be organized and stylized in a limitless number of ways. The ballots must conform to these design requirements:

1. Ballot size much be one of the available system options
2. Ballot must include a correctly formatted timing mark grid
3. Ballot must include an appropriately positioned QR code with its metadata
4. Ballot must use a specific bubble format

## Ballot Size

There are six valid ballot sizes. All are 8.5 inches in width, but vary in height:

| Name       | Length | Width |
| ---------- | ------ | ----- |
| Letter     | 11"    | 8.5"  |
| Legal      | 14"    | 8.5"  |
| Custom 17" | 17"    | 8.5"  |
| Custom 18" | 18"    | 8.5"  |
| Custom 21" | 21"    | 8.5"  |
| Custom 22" | 22"    | 8.5"  |

These lengths correspond to the length specified in the [Ballot Layout](hand-marked-ballots.md) within the election definition.

## Timing Mark Grid

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt="" width="563"><figcaption><p>Example of a timing mark-grid on letter-sized paper (scaled)</p></figcaption></figure>

The timing mark grid must exist on every ballot, front and back. The timing marks and page margins are strictly defined:

| Dimension                 |                |
| ------------------------- | -------------- |
| Timing Mark Width         | 3/16 in.       |
| Timing Mark Height        | 1/16 in.       |
| Page Margin (Top, Bottom) | 12pt (1/6 in.) |
| Page Margin (Left, Right) | 5mm            |

As for number of timing marks, there are always 34 columns. The number of rows varies based on the length of the ballot, and should be calculated by the formula **(# inches \* 4) - 3**. For example, a letter-sized ballot (11 inches) should have 41 rows of timing marks whereas a legal-sized ballot (14 inches) should have 53 rows of timing marks. The number of rows is inclusive of the top and and bottom row that are completely full of timing marks.

The timing marks should be aligned to the margins of the page and evenly spaced.

## QR Code Metadata

The ballot must include a QR code which contains key metadata about the ballot.

### QR Code Content

The QR code includes ballot metadata:

* Precinct Index - corresponds to a precinct in the election definition
* Ballot Style Index - corresponds to a ballot style in the election definition
* Page Number - page number within the ballot style
* Test Ballot Flag - indicates whether the ballot is a test ballot or an official ballot
* Ballot Type (Precinct, Absentee, or Provisional)

In addition, the QR code includes the [ballot hash](election-package/#election-package-and-ballot-hashes). The ballot hash ensures that the ballot was generated from the same election definition that will be used to interpret the ballot.

For full specifications on how to generate readable QR codes, view the [ballot encoder documentation](https://github.com/votingworks/vxsuite/tree/main/libs/ballot-encoder#hmpb-metadata-encoding) (**insert link updated)**.

### QR Code Placement

The interpreter looks for ballots in the top-right and bottom-left corners of the ballot within squares that are 1/4 of the width across.&#x20;

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt="" width="563"><figcaption><p>Highlighted areas must contain a QR code</p></figcaption></figure>

## Bubble Format

In order to be interpreted correctly, bubbles must meet the following dimensions:

| Dimension      | Measurement   |
| -------------- | ------------- |
| Width          | 0.20"         |
| Height         | 0.13"         |
| Border Radius  | 0.7"          |
| Line Thickness | 1px (0.265mm) |

<figure><img src="../.gitbook/assets/Screen Shot 2024-09-26 at 11.59.35 AM.png" alt="" width="563"><figcaption><p>Bubble example (not to scale)</p></figcaption></figure>

## Grid Coordinates

In the election definition, bubble positions and other ballot regions are specified relative to the grid coordinates. The ballot grid is an XY grid with the origin in the top-left corner. For example, the coordinate **(5, 3)** would correspond to the following position on the ballot:

<figure><img src="../.gitbook/assets/image (8) (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>

**Notes:**

* Coordinates correspond to the _centers_ of timing marks
* Coordinates specify the _center_ of bubbles
* Fractional coordinates are allowed

## Complete Example

Below is a complete ballot that, when paired with the appropriate election definition, could be interpreted within VxSuite:

<figure><img src="../.gitbook/assets/image (9) (1) (1).png" alt="" width="563"><figcaption><p>Valid ballot with timing marks, QR code, and bubbles</p></figcaption></figure>
