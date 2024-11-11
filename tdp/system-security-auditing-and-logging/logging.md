# Logging

All VxSuite applications use the same framework to log user actions, application processes, and errors. The logs are persisted to disk and can be exported by election managers or system administrators.&#x20;

## Application Log Events

VxSuite applications use a [shared logging library ](https://github.com/votingworks/vxsuite/tree/v4.0.0-release-branch/libs/logging)to capture required or otherwise important application log events. The core metadata for each application log event maps roughly to VVSG 2.0 standards, with some additional fields:

* **Log Event ID** - Internal identifier for each event. The full list of log event IDs with descriptions is included in the automatically generated [log documentation](https://github.com/votingworks/vxsuite/blob/v4.0.0-release-branch/libs/logging/VotingWorksLoggingDocumentation.md).
* **Log Event Type** - Describes whether the event is a status update or an action, and whether it originated with the user, application, or larger system. The full list of log event types with descriptions is included in the automatically generated [log documentation](https://github.com/votingworks/vxsuite/blob/v4.0.0-release-branch/libs/logging/VotingWorksLoggingDocumentation.md).
* **User** - If there was an authenticated user role at the time of a user action, describes the role as `system_administrator`, `election_manager`, `poll_worker` or `vendor`. If no user was authenticated, then `unknown`. If event does not originate from the user but rather automatically from the application or operating system, it will be `system`.&#x20;
* **Disposition** - For actions that can fail or succeed, `success` or `failure`. Otherwise `na` for not applicable.
* **Source** - Indicates where in the system's architecture the log came from, whether it be the frontend renderer, the frontend server, the backend server, a hardware daemon, or the operating system.
* **Message** - The log message itself, which may not be present if the log event ID sufficiently describes the event.
* **Other Metadata** - Other metadata can be freely included. For example, if a user adds manual tallies on VxAdmin, the metadata of those manual tallies will be included in the logging.
* **Time Written** - Timestamp of when the log was created.

## Log Management

The shared logging library formats the log events as JSON and pushes them to application processes' `stdout`. All `stdout` output from the application processes - both the application log events and any process output - is sent to the system's `logger` utility and assigned the tag `votingworksapp`.&#x20;

VxSuite uses `rsyslog`, an advanced implementation of the Syslog protocol, to centralize and manage logs from `votingworksapp` and other sources. `rsyslog` has advantages over the built-in Linux `syslog` implementation of the Syslog protocol, including JSON structured messages, advanced filtering, and increased performance. Using `rsyslog`, different types of logs are directed to different log files in `/var/log/votingworks/`:

<table><thead><tr><th width="172">Log File</th><th>Contents</th></tr></thead><tbody><tr><td><code>vx-logs.log</code></td><td><p></p><p>Key logs required by VVSG 2.0 or otherwise critical for understanding the behavior of the application or device, including:</p><ul><li>all application log events</li><li>USB device connection events</li><li>machine boot and shutdown events</li><li>all <code>sudo</code> actions</li><li>password events</li><li><code>dm-verity</code> events</li></ul></td></tr><tr><td><code>auth.log</code></td><td>All operating system authentication-related events. Note that this will not include voting system authentication events such as logging in with a smart card - these events are in <code>vx-logs.log</code></td></tr><tr><td><code>syslog</code></td><td>All other events emitted from the application or the operating system that do not fall into the other log files.</td></tr></tbody></table>

`vx-logs.log`  is the most important and informative file in most cases. The other files rarely need to be referenced.

Because each log file can grow very large, the application will rotate logs if necessary with the `logrotate` utility on each startup. Previous log files will be compressed and suffixed with a timestamp.&#x20;

Including the various log files and log rotation, below is an example of the list of log files that might appear on a device:

<pre><code><strong>/var/log/votingworks/vx-logs.log
</strong><strong>/var/log/votingworks/vx-logs.log-20241104.gz
</strong>/var/log/votingworks/vx-logs.log-20241105.gz
/var/log/votingworks/auth.log
/var/log/votingworks/syslog
/var/log/votingworks/syslog-20241105.gz
</code></pre>

## Default VotingWorks Log Format

```json
{
    "timeLogWritten":"2024-11-05T15:51:51.246232-08:00",
    "host":"VotingWorks",
    "source":"vx-scan-backend",
    "eventId":"auth-login",
    "eventType":"user-action",
    "user":"poll_worker",
    "message":"User logged in.",
    "disposition":"success",
}
```

The default VotingWorks log format is how logs are formatted when emitted from the application and how they appear in `vx-logs.log`. It is a direct mapping of the[#application-log-events](logging.md#application-log-events "mention") fields.

## CDF Log Format

Logs can be exported in CDF format, in which case the `vx-logs.log` file is replaced by a `vx-logs.cdf.json` file with the logging attributes mapped as follows:

<table><thead><tr><th width="304">CDF Attribute</th><th></th></tr></thead><tbody><tr><td>ElectionEventLog.GeneratedTime</td><td>ISO formatted timestamp of when logs were exported</td></tr><tr><td>ElectionEventLog.Device</td><td>List containing only the current device</td></tr><tr><td>Device.Type</td><td><p>The CDF <code>DeviceType</code> matching the type of machine:</p><ul><li>VxAdmin -> "ems"</li><li>VxScan -> "scan-single"</li><li>VxCentralScan -> "scan-batch"</li><li>VxMark -> "bmd"</li></ul></td></tr><tr><td>Device.Id</td><td>The serial number of the device</td></tr><tr><td>Device.Version</td><td>The software version e.g. "v3.1.2"</td></tr><tr><td>Device.Event</td><td>List of all events</td></tr><tr><td>Event.Id</td><td>A VotingWorks defined identifier for the type of event, such as "save-election-package-complete"</td></tr><tr><td>Event.Disposition</td><td>"success", "failure", "na", or "other"</td></tr><tr><td>Event.OtherDisposition</td><td>If the disposition is "other", the details appear here</td></tr><tr><td>Event.Sequence</td><td>The index of the log in the list of logs, zero-indexed</td></tr><tr><td>Event.TimeStamp</td><td>ISO formatted timestamp of when the event was logged</td></tr><tr><td>Event.Type</td><td>Log event type</td></tr><tr><td>Event.Description</td><td>Log pessage</td></tr><tr><td>Event.Details</td><td>JSON including the log source and any additional logging metadata</td></tr><tr><td>Event.UserId</td><td>The user at the time of the log</td></tr></tbody></table>
