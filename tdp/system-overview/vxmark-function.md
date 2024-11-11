# VxMark Function

VxMark is the system's ballot marking device. It allows all voters to make selections in various interaction modes, print their ballot, verify their ballot, and cast their ballot independently. VxMark is not a tabulator, and the cast ballots must be later tabulated at VxScan or VxCentralScan.

## Configuration

VxMark is configured with a signed [election package](election-package/#election-definition) exported from VxAdmin. The election definition defines the ballot styles that will be available to voters. The election definition also includes the translations defined for text on the ballot, while the [app strings](election-package/#app-strings) file contains the translations for other text shown on screen. The election package's [audio files](election-package/#audio-ids-and-audio-clips) are played for the voter in audio-mode.

{% hint style="info" %}
**User Manual Reference:** [Configure VxMark](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxmark/configure-vxmark "mention")
{% endhint %}

### Precinct Selection

VxMark is not fully configured until the election manager selects a precinct for the device. When polls are open, VxMark will only allow marking ballots in the ballot styles for the configured precinct. The election manager may configure VxMark to "All Precincts" in which case all ballot styles are available.

If the election definition only has one precinct, the precinct will be automatically selected.

The precinct selection can always be changed on VxMark by an election manager, even while polls are opened.

### Ballot Mode

After initial configuration, VxMark is in test ballot mode. The election manager can toggle between test ballot mode and official ballot mode. In official ballot mode, the ballots printed at VxMark will be official ballots. In test ballot mode, the ballots printed at VxMark will be test ballots.

Switching between ballot modes clears the printed ballot count and resets the polls to closed. The election manager can switch from test ballot mode to official ballot mode at any time.

### Unconfiguring

VxMark can be unconfigured by an election manager or system administrator.

## Polls Management

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

After configuration, polls are initially closed. When polls closed, voting is not allowed on VxMark.&#x20;

Poll workers open the polls to allow voting. Once polls are opened, polls can only return to the initial polls closed state while remaining configured by switching between test and official ballot mode.

Poll workers close the polls when voting should no longer be allowed. Polls are closed until VxMark is unconfigured or switched from one ballot mode to another, with one exception discussed below.

VxMark also allows poll workers to pause voting a.k.a. suspend the polls. While voting is paused, no voting sessions can be started. Voting can be resumed, after which the polls are back in the standard polls opened state. Pausing voting might be used in an early voting model between voting days or, in the case of an emergency, to pause voting while the emergency is resolved. The poll worker may chose to close polls directly from voting paused instead of resuming voting.

If the polls have been closed, the only possible way for the polls to be re-opened is if a system administrator resets the polls to paused. Only the system administrator may do this - poll workers and election managers cannot - per the allowance in VVSG 2.0 1.1.7-E. Once polls have been reset to paused by the system administrator, voting may be resumed by a poll worker. The goal of this flow is to allow voting to continue after a poll worker has prematurely closed the polls.

{% hint style="info" %}
**User Manual Reference:** [Open/Close Polls](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxmark/open-close-polls "mention")
{% endhint %}

## Voting Sessions

When polls are opened, poll workers can enable voting sessions on behalf of voters. The poll worker selects one of the available ballot styles and loads a blank piece of thermal paper into the front input tray.

The voter navigates through the contests on their ballot style sequentially, with controls to advance to the next contest or go back to the previous contest. The contest information presented to the voter includes the contest title, the contest district, the number of selections allowed, the number of selections remaining, the contest options, the candidates' parties if applicable, and the descriptions of any ballot measures (VVSG 2.0 7.3-C).

Voters may leave contests blank or undervoted but are prevented from overvoting contests. If the voter attempts to mark an overvote, they will be presented a warning and instructed to deselect another selection if they want to make the new selection (VVSG 2.0 7.3-H). Previous selections are never automatically deselected.

If the contest allows write-ins, they may input a write-in name via a virtual keyboard.

After working through the entire ballot, the voter will then review all their selections. Any undervotes will be flagged for the voter (VVSG 2.0 7.3-I) but may be ignored. If the voter does want to make any changes, they can navigate back to any contest, make changes, and return to the review stage (VVSG 2.0 7.3-F). Once the voter is satisfied with their selections, they may print their ballot.

The thermal printer prints a ballot, presents it to the voter, and prompts them to once again review their selections. This final review differs from the initial review in two ways. First, the printed ballot is being physically presented to the user which creates a voter-verified paper trail. Second, the selections being  reviewed are a result of the actual interpretation of the ballot rather than simply the selections made by the voter. As a result, even when a voter is unable to verify their printed paper ballot visually they are still able to verify the ballot through another interaction mode. Once the voter is satisfied with their second round of review, they may cast their ballot which is ejected into the attached ballot box.

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

If the voter finds a problem in their ballot during the final review stage, they must spoil the ballot. They are prompted to get help from a poll worker who can help them spoil their ballot and load a new, blank sheet. Once the blank sheet is loaded, the voter returns to the initial review stage from which they can edit selections before reprinting, reviewing, and casting their ballot.

While the paper ballot is being presented to the voter, they are supposed to leave it in the scanner so it can be ejected into the ballot box when they cast their ballot. Many voters will naturally remove the ballot from the scanner, however, and cannot cast their ballot until they re-insert the ballot. When they do insert their ballot, it is scanned again and they are returned to the final review stage.

It's possible that a voter removes their ballot and does not re-insert it before the voting session times out. In this case, it's possible for a poll worker to initialize a session by re-inserting an already printed ballot rather than by selecting a ballot style. The already printed ballot is scanned and the voter is dropped directly on the final review screen.

If a re-inserted ballot is somehow not compatible with the machine - wrong election, wrong precinct or wrong ballot mode - the user is alerted and the ballot is rejected out the front.

{% hint style="info" %}
**User Manual Reference**: [Voting Sessions](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxmark/voting-sessions "mention")
{% endhint %}

## Display Formats & Interaction Modes

VxMark supports voting sessions in various display formats and interaction modes.

{% hint style="info" %}
**User Manual Reference:** [Voting Session Language & Settings](https://app.gitbook.com/s/JtZutzGTdCzsGITrdiph/vxmark/voting-session-language-and-settings "mention")
{% endhint %}

### Visual and Enhanced Visual Formats

The voting session begins in visual mode with the following default settings:

* **Text Size** - Medium, which corresponds to between 14pt - 16pt, meeting the default text size requirement specified in VVSG 2.0 7.1-G.
* **Contrast** - Medium, which is at least a 10:1 contrast for all informational elements, meeting the default contrast requirement specified in VVSG 2.0 7.1-C

The voter can update the **Text Size** to Small, Medium, Large, or Extra-Large, which map to the four discrete text sizes defined in VVSG 2.0 7.1-G. Changing the text size changes the size of all informational elements including buttons, icons, and layout (VVSG 2.0 7.1-H) because all such elements are sized relative to the base font size. The font is always sans-serif (VVSG 2.0 7.1-J).

If there's too much content on a page to fit all on screen at once, which happens most commonly in large or extra-large text size, the interface introduces a large "More" button to indicate there are more contest option to scroll through. The interface never lays out content in a way which requires horizontal scrolling.

The voter can update the **Contrast** from medium contrast to low contrast, high contrast with black background, or high contrast with white background corresponding to the contrast options specified in VVSG 2.0 7.1-D. The contrast changes apply to all elements on screen.

In addition to text, color and icons are used on screen to guide voters. In conformance with color conventions (VVSG 2.0 7.1-E), red indicates danger, yellow indicates warning, and green indicates success. For example, choosing to spoil one's ballot is a red button. Purple is generally used as the primary color to indicate the recommended next step. In high contrast modes, the interface is entirely black and white to support the 20:1 contrast ratios. Icons are used on buttons to provide an additional visual cue, but are always paired with text (VVSG 2.0 7.3-L).

Ending a voting session will automatically reset all display settings to defaults (VVSG 2.0 7.1-A). The voter can change or reset the display settings to defaults at any time (VVSG 2.0 7.1-B).

In visual mode, when a voter makes a selection it is indicated in three ways:

* Highlighting the selection in a contrasting color
* Updating the icon from an unchecked to a checked box
* Decrementing the number of remaining votes allowed shown on screen

Once a voter has used all their votes in a race, the progress button at the bottom of the screen to advance to the next race is also highlighted to encourage the voter to proceed.

### Touch Interaction Mode

Voters usually choose to use the touchscreen to vote. The voter taps buttons to move between contests and through the stages of the voting flow. The voter taps list items on each contest page in order to make selections. Touch areas never overlap and are sized to meet minimums described in VVSG 2.0 7.2-I. Touch areas require that the user's touch begins and ends within the touch area to activate, meaning that dragging a finger across a touch area will not activate the touch area, in order to avoid accidental activation (VVSG 2.0 7.2-H).

When there's more content on a page than can fit on one screen, the voter can scroll through the screen in one of two ways. First, they can tap the "More" button which acts as both the visual indicator that there are more contest options or contests. Second, they can use a swiping motion on the screen to move up or down. Swiping to see more contest options or contests is VxMark's only touch screen gesture. It cannot be used horizontally to navigate between contests or pages and  (VVSG 2.0 7.2-E).

### Limited Dexterity Mode - Accessible Controller

VxMark has a permanently attached accessible controller that can be used to navigate the ballot instead of using the touchscreen directly. The left and right buttons are used to navigate between contests and other screens while the up and down buttons are used to navigate between contest options or contests within each screen. The controller has a help button which will navigate to a help interface that explains the function of each button on the controller when pressed.

The currently focused element on screen is highlighted in visual mode or read aloud in audio mode. When navigating through selections on a screen large enough to be scrollable, the screen will automatically scroll to keep the focused element in view.&#x20;

The accessible controller is integrated with the application via a hardware daemon that is always running. The daemon is continuously listening for input events from the controller. Each event is converted into virtual keyboard presses which are then handled by the frontend rendering agent just as a web browser might handle arrow key inputs.

### Limited Dexterity Mode - PAT Input

VxMark has a PAT (personal assistive technology) input port into which a voter can plug in their own two-switch adaptive input such as a sip-and-puff device. When a PAT input is attached during a voting session, VxMark will enter a calibration flow where the voter will map their two inputs to "move" and "select." Different voters can calibrate their sip & puff devices differently such that sip is "move" for one and "select" for another.

Once calibrated, the voter can use the two inputs to navigate through the ballot. The "move" input advance the focus on screen to the next element and the "select" input is the equivalent of a tap in touch interaction mode. Just as with the accessible controller, the currently focused element on screen is highlighted in visual mode or read aloud in audio mode.&#x20;

The PAT input is integrated with the application via a hardware daemon that is always running. The daemon is continuously listening for input events from an attached device. Each event is converted into virtual keyboard presses which are then handled by the frontend rendering agent just as a web browser might handle `Tab` and `Enter`.&#x20;

### Audio Format

As an alternative to the visual formats, the voter can listen to their ballot in an audio format. VxMark includes a headphone port and headphones which, when attached, will automatically play audio to guide the voter's ballot navigation. The audio includes information about the election, contests, and contest options equivalent to the information displayed on screen in visual mode. The audio also includes prompts and explanations for how to navigate the ballot that are equivalent to the cues in layout and highlighting on screen in visual mode. These instructions include but are not limited to:

* how to start voting
* how to make selections in a contest
* how to navigate the review screens
* how to use the accessible controller

The voter can adjust volume up and down or speech rate up and down with buttons on the accessible controller. Volume and rate defaults and options are calibrated according to VVSG 2.0 7.1-K. The voter can also pause and resume audio with a button on the accessible controller.

Blind or visually impaired voters can use the audio track to review their printed ballot. The printed ballot is scanned and interpreted on its way out of the printer, and the resulting interpretation is the basis for the audio played in the second review state. As a result, blind or visually impaired voters are able to verify their paper ballots just as seeing voters are able to verify their paper ballots.

### Language Support

VxMark supports switching the language for the current voting session to any language supported in the current election package. When the language is changed, all text on the ballot, all text shown on screen, and text read in audio mode to guide the voter will switch to the new language. The language can be changed at any time during a voting session. The language selection resets automatically after each voting session or can be reset by the voter at any time..

If a language other than English is set when printing the ballot, the ballot will show all information in both the current language - for the purpose of the voter's review - and in English - for ease of adjudication and audits.

## Printer Access Control













