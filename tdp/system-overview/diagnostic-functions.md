# Diagnostics

All VxSuite components have a diagnostics interface accessible to system administrators and election managers that allows a user to monitor or test key components. Diagnostic information is shown to the user and can be exported as a PDF readiness report.

When a test is performed, the system logs the result and creates a diagnostic record which includes the outcome of the diagnostic, pass or fail. The outcome and date of the most recent diagnostic is displayed on the readiness report. One possible use case of the readiness report is to run all diagnostics before an election and then produce a readiness report that confirms all tests passed.&#x20;

## Common Diagnostics

### Storage

Retrieves the current amount of disk space used and disk space available for the application. The displayed total disk space will not be as large as the actual disk because some space is reserved for the system. The disk space usage will not always return to 0% after clearing election data because the database may not have liberate that disk space back to the operating system, but the space will be reused once more election data is loaded.

### Battery

For components with internal batteries - VxAdmin and VxCentralScan - the operating system is polled for battery status. The application will report the current charge level and whether or not the battery is currently charging.

### Configuration

#### Election Identifier

If there is an election configured on the machine, it will display the election title and hash.

#### Ballot Styles

For precinct equipment, the list of ballot styles will include only those appropriate for the current precinct configuration. For central equipment, the list of ballot styles will be all ballot styles in the election. The languages for each ballot style are also enumerated

#### Precinct

For precinct equipment - VxScan and VxMark -  the currently configured precinct will be shown, if any.

#### Mark Thresholds

For scanners - VxScan and VxCentralScan - the currently configured mark and write-in area thresholds will be shown. The thresholds reflect what was set in the [system settings](election-package/#system-settings).

## VxAdmin Diagnostics

### Printer

The toner level and any alerts from the printer are displayed, such as sleep mode, paper jams, or hardware malfunctions. The user may perform a test print, which will send a mock report to the printer. The user inspects the printed document and confirms whether the test print was successful or failed.

## VxCentralScan Diagnostics

### Batch Scanner

The user may perform a test scan, which requires that a blank white sheet of paper be scanned. The scanned image is broken up into small cells and each cell is checked for the percent of black pixels after binarization. If that percent is more than slightly over 0%, that cell is flagged and the entire diagnostic fails. The goal of the diagnostic is catch any defects in the scanned images, such as streaking produced by a dirty scanner.

<div>

<figure><img src="../.gitbook/assets/3d3eeff3-0eda-48fd-be9d-8edda7abdd2d-front_debug_diagnostic.png" alt=""><figcaption><p>Passed</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/0dc29646-3c6a-4abd-9d2d-ae1b03a3b4ad-front_debug_diagnostic.png" alt=""><figcaption><p>Failed</p></figcaption></figure>

</div>

## VxScan Diagnostics

### Embedded Scanner

The user may perform a test scan, which requires that a blank white sheet of paper be scanned. The scanned image is broken up into small cells and each cell is checked for the percent of black pixels after binarization. If that percent is more than slightly over 0%, that cell is flagged and the entire diagnostic fails. The goal of the diagnostic is catch any defects in the scanned images, such as streaking produced by a dirty scanner.&#x20;

The test scan process is identical to that for VxCentralScan, and the images above apply.

### Thermal Printer

The user may test the printer by printing a test page. After the print, the user must indicate whether the page printed successfully or not. The diagnostic available in the diagnostics interface is identical to that which election managers are encouraged to run after loading paper, and the outcome is recorded in either case.

The diagnostics page will also display details about any printer errors if the printer is in an error state.

### Speaker

The user may test the speaker by triggering the chime sound and confirming whether they heard the chime or not.&#x20;

## VxMark Diagnostics

### Printer-Scanner

The user may perform a test of the printer-scanner which mocks the ballot flow during a voting session:

1. User loads thermal paper
2. Mock ballot is printed onto paper
3. Mock ballot is scanned and presented in the front input tray
4. Mock ballot is ejected into the ballot box

A successful test indicates that the printer and scanner can properly produce and handle ballots during a voting session.

### Accessible Controller

The user may perform a test of the accessible controller which validates that each button on the controller is producing the expected signal. The flow guides the user through pressing each button.

### PAT Input

The user may perform a test of the PAT input, which is simply confirms that a PAT device can be successfully calibrated as it would be during a voting session.

### Front Headphone Input

The user may perform a test of the front headphone input by connecting headphones and triggering a chime. The user must indicate whether they heard the chime or not, corresponding to a pass or fail respectively.























