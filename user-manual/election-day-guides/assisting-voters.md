# Assisting Voters

## Casting Ballots

VxScan is ready to accept a new ballot whenever it displays Insert Your Ballot.

<figure><img src="../.gitbook/assets/image (21).png" alt="" width="375"><figcaption></figcaption></figure>

A voter can then push their ballot onto the tray and into the scanner. When a ballot is properly inserted, the scanner will grip the ballot. If a ballot is inserted at an angle, the scanner may push the ballot back into the voter's hands without scanning, the voter should simply re-insert their ballot. VxScan will then scan the ballot by pulling it in and show the following screen.

<figure><img src="../.gitbook/assets/30-scan-processing-screen.png" alt="" width="375"><figcaption></figcaption></figure>

If the ballot has no issues, the ballot will go into the ballot box and the screen will show that the ballot has been counted. Notice the Ballots Scanned count goes up.

<figure><img src="../.gitbook/assets/image (22).png" alt="" width="375"><figcaption></figcaption></figure>

After a few seconds, VxScan will return to the Insert Your Ballot screen in preparation for the next voter. &#x20;

If the ballot was not counted because of an issue, the scanner will hold the ballot. There could be any of the following issues with the ballot depending on state law or rule.

### Overvoted Ballots

If the scanner recognizes more than the allowed number of votes for a particular race. For example, a voter marked two candidates in a race where they must make a single choice. If the voter would like to correct their error, they should select _`Return Ballot`_ and VxScan will return the ballot to the voter. If the voter would like to count the ballot as is, they should select _`Cast Ballot As Is`_ and then confirm by selecting _`Yes, Cast Ballot As Is`_.  All valid votes will be counted in correctly voted contests but the overvoted contest will be excluded.

<figure><img src="../.gitbook/assets/image (23).png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
An overvote will also be detected when a candidate is marked and writing is detected on the write-in line for the same contest if it exceeds the number of allowed votes (when required by law or rule). This is true even if the bubble is not marked.&#x20;
{% endhint %}

### Blank Ballots

If a state requires notification to the voter that a ballot has no selections marked (blank), the voter will be prompted to review their ballot.

The voter may have circled or underlined the names of their choices instead of filling in the bubbles. Or the voter may have used a writing utensil whose marks are ignored by the scanner, like a highlighter. VxScan will warn the voter that their ballot appears blank.

<figure><img src="../.gitbook/assets/32-scan-warning-screen-blank-ballot.png" alt="" width="375"><figcaption></figcaption></figure>

If the voter would like to correct their error, they should select _`Return Ballot`_ and VxScan will return the ballot to the voter. If the voter would like to count the ballot as is, they should select _`Cast Ballot As Is`_ and then confirm by selecting _`Yes, Cast Ballot As Is`_. No votes will count on a blank ballot.

### Undervotes

If a state requires notification to the voter that a specific contest has no selections marked (undervote), the voter will be promoted to review their ballot. If many contests are undervoted, select _`View contests`_ to see each contest.

<figure><img src="../.gitbook/assets/35-scan-warning-screen-undervote-1-contest.png" alt="" width="375"><figcaption></figcaption></figure>

If the voter would like to correct their error, they should select _`Return Ballot`_ and VxScan will return the ballot to the voter. If the voter would like to count the ballot as is, they should select _`Cast Ballot As Is`_ and then confirm by selecting _`Yes, Cast Ballot As Is`_. Votes for all contests with valid votes will be counted.

### Multiple Corrections

If a voter has both undervotes and overvotes on their ballot and the state requires review of both, the Review Your Ballot screen will appear. Select _`View contests`_ to see each contest that was undervoted or overvoted.&#x20;

<figure><img src="../.gitbook/assets/33-scan-warning-screen-mixed-overvotes-and-undervotes.png" alt="" width="375"><figcaption></figcaption></figure>

If the voter would like to correct their errors, they should select _`Return Ballot`_ and VxScan will return the ballot to the voter. If the voter would like to count the ballot as is, they should select _`Cast Ballot As Is`_ and then confirm by selecting _`Yes, Cast Ballot As Is`_. Votes for all contests with valid votes will be counted.

### Adjusting Color and Size

Simple changes to the screens color and size can be very helpful for voters with low vision and other cognitive disabilities. Selecting _`Settings`_ in the upper right hand corner of the screen provides the voter with different options.

<figure><img src="../.gitbook/assets/image (13).png" alt="" width="375"><figcaption></figcaption></figure>

**Text and Screen Color**

Select _`Color`_ to change the background and/or text color and select _`Text Size`_ to change the text size.

Four different color options are available for users. While we provide a short description of who may benefit most from these different options, please note that the user likely knows what setting is best for their disability.&#x20;

**White text, black background** - used by a person that finds white backgrounds too bright due to visual disabilities. May also be easier to read when room lighting causes a glare on the screen.

**Gray text, dark background** - used by a person needing lower contrast. For example, a person with dyslexia may find the screen quieter.

**Dark text, light background** - as the default this setting will be used by most people.

**Black text, white background** - used by people who need the highest contrast because of light vision or color perception disabilities or aging.

<figure><img src="../.gitbook/assets/color.png" alt="" width="375"><figcaption></figcaption></figure>

#### Text Size

The default text size is _`Medium`_.  A user can select _`Small`_, _`Large`_, or _`Extra-Large`_ based on their preferences.  Select _`Done`_ to save the selection.&#x20;

<figure><img src="../.gitbook/assets/text-size.png" alt="" width="375"><figcaption></figcaption></figure>

### Language

If a jurisdiction provides language options to voters, a voter may select that language by selecting _`English`_.

<figure><img src="../.gitbook/assets/image (14).png" alt="" width="375"><figcaption></figcaption></figure>

Next, they'll select the language of their choice and select _`Done`_.&#x20;

<figure><img src="../.gitbook/assets/language.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="warning" %}
All selections above are made for a specific voting session and will reset with the next voter.
{% endhint %}
