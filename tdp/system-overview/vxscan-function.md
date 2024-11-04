# VxScan Function

VxScan is the system's precinct scanner into which voters cast their ballots directly.

## Configuration

VxScan is configured with a signed [election package](election-package/#election-definition) exported from VxAdmin. The election definition includes the ballot layouts necessary for interpreting ballots and the system settings which indicate what type of ballot issues (e.g. overvotes) require adjudication.&#x20;

{% hint style="info" %}
**User Manual Reference:** [Configure VxScan](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxscan/configure-vxscan "mention")
{% endhint %}

### Precinct Selection

VxScan is not fully configured until the election manager selects a precinct for the device. When polls are open, VxScan will only accept ballots for the configured precinct. If ballots for other precincts are cast, they will be rejected. The election manager may configure VxScan to "All Precincts" in which case ballots for all precincts will be accepted.&#x20;

If the election definition only has one precinct, the precinct will be automatically selected and the precinct will not be editable.

Once polls are opened and ballots are cast, the precinct can no longer be changed. If polls are opened but ballots have not yet been cast, the precinct can still be changed but it will result in the polls resetting to closed. Resetting the polls to closed forces a poll worker to re-open the polls, which reprints the polls opened report with the new, correct precinct configuration.

### Ballot Mode

After initial configuration, VxScan is in test ballot mode. The election manager can toggle between test ballot mode and official ballot mode. In official ballot mode, only official ballots can be scanned and exported CVRs will be official ballot CVRs. In test ballot mode, only test ballots can be scanned and exported CVRs will be test ballot CVRs. If `allowOfficialBallotsInTestMode` is set in the [system settings](election-package/#system-settings), official ballots will be allowed in test mode but exported CVRs will still be test CVRs.

Switching between ballot modes clears all scanned ballot data and resets the polls to closed. The election manager can switch from test ballot mode to official ballot mode at any time. When in official ballot mode after ballots have been scanned, the election manager can only switch back to test ballot mode if the CVRs have been synced to the USB drive.

### Unconfiguring

VxScan can be unconfigured by an election manager or system administrator. If ballots have been scanned in official ballot mode, an election manager can only unconfigure the machine after scanned ballot data has synced to a USB drive. System administrators can unconfigure the machine at any time.

## Hardware Management

### Printer Management

VxScan includes an embedded A4 thermal roll printer which is used to print polls reports. The application is regularly polling the printer for status, which is one of the following:

<table><thead><tr><th width="172">Status</th><th width="282">Meaning</th><th>Effect</th></tr></thead><tbody><tr><td>Ready</td><td>Platen is attached and paper is detected</td><td>Application may print normally</td></tr><tr><td>No Paper</td><td>Platen is attached but no paper is detected</td><td>Printing disabled. A warning will be shown on poll worker screens. </td></tr><tr><td>Cover Open</td><td>Platen is not attached</td><td>Printing disabled. If the polls are open, a warning will be shown.</td></tr><tr><td>Error</td><td>Most likely the printhead has overheated, but other hardware errors are possible. Details available in diagnostics interface.</td><td>Printing disabled. Poll workers will not be able to operate the polls, but election managers and system administrators can still authenticate for diagnostics.</td></tr></tbody></table>

During a polls transition, a polls report is [generated](software-overview.md#document-creation) and gradually sent to the printer. Documents are A4 width but of indefinite length depending on the number of contests on the ballot styles at the precinct. If the printer encounters an error or runs out of paper in the middle of a print, the poll worker will be prompted to wait or to replace the thermal roll in order to continue printing. The previous document will reprint from the beginning. In most cases, poll workers do not have to install the thermal paper roll.&#x20;

Election managers normally install the thermal paper rolls via a guided flow. They will be prompted to remove the platen, install the paper, and re-install the platen. Whenever an election manager installs a thermal paper roll, they are also prompted to print a test page. The main goal of the test print is to ensure that the election manager installed the roll in the correct orientation as it is one-sided and, if reversed, will not print anything.

The printer roll can be loaded at any time, including when VxScan is off. It only requires opening the access door which may be sealed.

{% hint style="info" %}
**User Manual Reference:** [Printer](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxscan/election-manager-settings#printer "mention")
{% endhint %}

### Scanner Management

VxScan scans ballots with an embedded A4/Letter document scanner which produces double-sided ballot images. The application manages its transitions between hardware states (waiting, accepting, etc.) and controls when it will or will not accept ballots.

The embedded scanner includes a multi-sheet detector (MSD) which allows the application to reject cases of voters feeding in multiple ballots at a time. The multi-sheet detection must be calibrated at the beginning of an election based on the thickness of the ballot paper. The double sheet detection calibration flow is exposed in the election manager menu. The election manager can choose to disable double sheet detection, but it is enabled by default.

The scanner's cover can be opened for cleaning, during which scanning will be disabled and the application will show a warning on screen if the polls are open.

### Audio Management

VxScan makes noises whenever a ballot is accepted or rejected. The ballot accepted sound is a pleasant chime and the ballot rejected sound is a jarring beep. Election managers can toggle sounds on or off.

## Polls Management

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

After configuration, polls are initially closed. When polls closed, ballots cannot be cast.&#x20;

Poll workers open the polls to allow casting ballots. Once polls are opened, polls can only return to the initial polls closed state while remaining configured in two ways. First, switching from test ballot mode to official ballot mode will reset the polls. Second, in cases where the polls are open but no ballots have been cast, the precinct can still be changed which will also reset the polls to closed. Both of these actions can be performed by election managers but not poll workers. While polls are open, ballots can be inserted by voters, scanned, and tabulated.

Poll workers close the polls when ballots should no longer be cast. After polls have been closed, the scanner will not accept ballots and the polls cannot be opened again. Polls are closed until VxScan is unconfigured or switched from one ballot mode to another, with one exception discussed below.

VxScan also allows poll workers to pause voting a.k.a. suspend the polls. While voting is paused, the scanner will not accept ballots. Voting can be resumed, after which the polls are back in the standard polls opened state. Pausing voting might be used in an early voting model between voting days or, in the case of an emergency, to pause voting while the emergency is resolved. The poll worker may chose to close polls directly from voting paused instead of resuming voting.

If the polls have been closed, the only possible way for the polls to be re-opened is if a system administrator resets the polls to paused. Only the system administrator may do this - poll workers and election managers cannot - per the allowance in VVSG 2.0 1.1.7-E. Once polls have been reset to paused by the system administrator, voting may be resumed by a poll worker. The goal of this flow is to allow voting to continue after a poll worker has prematurely closed the polls.

{% hint style="info" %}
**User Manual Reference:** [Opening Polls](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/election-day-guides/opening-polls "mention"), [Closing Polls](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/election-day-guides/closing-polls "mention"), [Additional Poll Worker Actions](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxscan/additional-poll-worker-actions "mention")
{% endhint %}

## Scanning

Scanning can begin once VxScan is fully configured and polls are open. If any user authenticates, scanning will be disabled until they remove their card. If CVRs are not synced to the USB drive, scanning will be disabled until a sync is complete.

While scanning is enabled, the scanner will grab and scan paper as soon as it is detected. The scanned image will be [interpreted](ballot-interpretation.md) while the ballot is still being held by the scanner. If the ballot is interpreted successfully and contains no errors, it will be ejected into the ballot box with a chime and the screen will inform the voter that their ballot has been cast.&#x20;

If the ballot cannot be interpreted, it will be rejected toward the voter. Interpretation can fail if the ballot is not a valid [hand marked ballot](hand-marked-ballots.md) or if the ballot enters the scanner at too much of an angle, although the paper path normally prevents significant skew. If the ballot is interpretable but is invalid due to a mismatching election, precinct, or ballot mode, it will also be rejected toward the voter.

If the ballot is interpreted and valid, but contains some voter error, the scanner will hold the ballot out of view while the errors are presented to the voter on screen. The types of errors that are flagged are determined by the `precinctScanAdjudicationReasons` set in the [system settings](election-package/#system-settings). Possible options are overvotes, undervotes, and blank ballots. In the case of overvotes or undervotes, the specific list of affected contests will be listed. The voter has the option to return the ballot to themselves or to cast it despite warnings. If there's an overvote and `disallowCastingOvervotes` is set in the system settings, however, the ballot can only be returned.

If the `precinctScanAdjudicationReasons` includes adjudicating unmarked write-ins, which are marks in the write-in space with the associated bubble unmarked, those unmarked write-ins will be included when determining whether a contest contains an overvote. At the same time, it will be considered an undervote. For example consider a vote for one contest. If the voter only fills in an unmarked write-in, it will be considered an undervote. If the voter fills in a bubble and a separate unmarked write-in, it will be considered an overvote when warning the voter. Warning in both these cases encourages the voter to clarify their ambiguous marks. When it votes are tallied, however, unmarked write-ins are always  considered undervotes at VxScan.

Once the ballot is cast, whether immediately after interpretation or after the voter confirms to cast a ballot with errors, the image and interpretation are both saved to disk and exported to the inserted USB drive as a CDF CVR. The sheet count shown on screen will increment accordingly.

{% hint style="info" %}
**User Manual Reference**: [Assisting Voters](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/election-day-guides/assisting-voters "mention")
{% endhint %}

## Cast Vote Records

VxScan exports cast vote records to the inserted USB drive continuously, after every ballot is cast, in order to avoid a lengthy export at the end of the day. All cast vote records include ballot images and images of rejected ballots are also included. If there is no USB drive in VxScan, ballots cannot be cast. If the CVRs on the USB drive are not in sync with record of ballots on disk, VxScan requires a poll worker or election manager to sync the CVRs to the USB drive. This normally occurs when a USB drive is swapped out after ballots have already been scanned.

Continuous export can be disabled by an election manager if need be, for example if a USB drive turns out to be slow or no USB drive is available. If continuous export is disabled, VxScan can be used without a USB drive inserted.

CVRs can be exported directly from the election manager menu, in which case they export all at once.

{% hint style="info" %}
**User Manual Reference**: [CVRs and Logs](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxscan/election-manager-settings#cvrs-and-logs "mention")
{% endhint %}

## Reports

On polls open, polls closed, voting paused, and voting resumed, VxScan prints a report via the thermal printer. The poll worker has the option to reprint additional report as many times as they need. The latest polls report can be cast as long as no ballots have since been cast. For example, the polls opened report can be printed as long as zero ballots have been cast. The polls closed report can be printed indefinitely, because no ballots can be cast after polls are closed. Reports will have both the timestamp of the polls transition and of the report printed, so reports printed at a later time are distinguishable.&#x20;

For details about the format of the polls reports, see [vxscan-polls-reports.md](vxscan-polls-reports.md "mention").

For polls opened and polls closed reports, the vote interpretations of all ballots are tallied together. In the case of polls opened reports, the tallies should always be zero forming a zero report. It is impossible to have any ballots scanned already at the time of polls are opened, because the scanner is disabled until polls are opened. Pursuant to VVSG 2.0 1.1.3-B, however, in the impossible event that non-zero totals are detected on the machine when the poll worker attempts to open the polls, an error will be presented to the poll worker and they will be unable to open the polls.&#x20;

Tallies for the polls closed report are created by iterating through the data store's table of cast vote records and forming totals of votes for contest options, undervotes, overvotes, and total ballots cast. The process is the same as on VxAdmin but with far fewer steps because there are no write-in adjudication results to consider and no manual tallies. All marked write-ins are grouped as a generic "Write-In" count in reports. All unmarked write-ins are considered as undervotes.

For voting paused and voting resumed reports, only a total ballot count is included as opposed to vote tallies.

