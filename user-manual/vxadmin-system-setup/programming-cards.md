# Smart Cards and User Roles

{% hint style="info" %}
Smart card programming can only be done by a system administrator.
{% endhint %}

## Overview

Smart cards are used to configure and operate equipment. It's the same technology as the chip in your credit card, but is instead used to provide election administrators and poll workers a secure means to configure and operate the equipment. There are three user roles and cards: system administrator, election manager, and poll worker**.**

<figure><img src="../.gitbook/assets/image (678).png" alt="" width="375"><figcaption><p>Smart cards</p></figcaption></figure>

### System Administrator

System administrator cards allow an election administrator to load an election definition, program smart cards, and remove the election definition from VxAdmin.

System administrator cards should only need to be used at the very beginning and very end of an election. Keep this card in a secure location when not in use and in between elections.

{% hint style="info" %}
System Administrators should be an election administrator or their designee who is in charge of the voting system.  The technical skill level required for this role is a 6-hour training session provided by VotingWorks.
{% endhint %}

### Election Manager&#x20;

Election manager cards allow election administrators to use central system devices and configure precinct system devices. Election managers are responsible for:

* configuring/unconfiguring precinct equipment
* preparing machines for L\&A&#x20;
* preventative maintenance tasks
* general equipment troubleshooting
* centrally scanning ballots
* tallying CVRs
* adjudicating write-ins
* entering manual tallies
* printing and saving results

Election manager cards should only be used by election administrators and should be kept secure at all times.

{% hint style="info" %}
Election managers should be an election administrator or their designee who is in charge of the voting system.  The technical skill level required for this role is a 4-hour training session provided by VotingWorks.

The technical skill level required for an election manager only operating the VxCentralScan is a 1-hour training session provided by the election official.
{% endhint %}

### Poll Worker Cards

Poll worker cards allow poll workers to manage election day precinct tasks, including:

* opening the polls
* pause/resume the polls
* closing the polls
* printing precinct tally reports

Every precinct will need at least one poll worker card in order to operate the polls.

{% hint style="info" %}
A poll worker should be designated by the election administrator to operate the voting equipment during open voting periods.  The technical skill level required for this role is a 1-hour training session provided by the election official.
{% endhint %}

## Programming Cards

For each election, you will create election manager and poll worker cards specifically for that election. Smart cards can be created quickly and easily with VxAdmin by logging in with a System Administrator Card and selecting Smart Cards from the side menu.

<figure><img src="../.gitbook/assets/smart-cards-screen-emph.png" alt="" width="563"><figcaption><p>Smart cards screen without card inserted</p></figcaption></figure>

You will use the smartcard reader in the lower lefthand side of your VxAdmin laptop to program a card. Simply insert the card of your choice and select the correct button for the card.

<figure><img src="../.gitbook/assets/image (140).png" alt="" width="563"><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/smart-cards-blank.png" alt="" width="563"><figcaption><p>Smart cards screen with blank card</p></figcaption></figure>

When creating an election manager or system administrator card, the screen will show you a unique PIN for that card. Keep the PIN secure. When creating a poll worker card, the screen will simply confirm the card is created.

<div>

<figure><img src="../.gitbook/assets/smart-cards-sa-programmed (1).png" alt=""><figcaption><p>System administrator card programmed</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/smart-cards-em-programmed (1).png" alt=""><figcaption><p>Election manager card programmed</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/smart-cards-pw-programmed (1).png" alt=""><figcaption><p>Poll worker card programmed</p></figcaption></figure>

</div>

{% hint style="info" %}
If VxAdmin is not configured with an election, you will only be able to program system administrator cards because election manager and poll worker cards are election-specific.
{% endhint %}

## Modifying and Unprogramming Cards

If you insert an already programmed card, you will be presented with options to modify the card.

<div>

<figure><img src="../.gitbook/assets/smart-cards-sa-existing.png" alt=""><figcaption><p>Modifying a system administrator card</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/smart-cards-em-existing.png" alt=""><figcaption><p>Modifying an election manager card</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/smart-cards-pw-existing.png" alt=""><figcaption><p>Modifying a poll worker card</p></figcaption></figure>

</div>

**Unprogram Card** will remove the election configuration from the card, after which it can be programmed for a new election. System administrator cards cannot be unprogrammed.

**Reset Card PIN** will reset the card PIN. The old PIN will no longer be valid. Note the new PIN and keep it secure. The PIN can only be reset on cards that match the current election.
