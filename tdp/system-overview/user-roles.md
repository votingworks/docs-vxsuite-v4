# User Roles

VxSuite has four authenticated user roles. Authentication is performed with JCOP4 Java Cards, a security-oriented type of smart card. Each card is programmed with a single role and, in most cases, a PIN for two-factor authentication. Details of the authentication system can be found in the System Security section of the TDP (**insert link**).&#x20;

## Poll Worker Role

The poll worker role is the lowest privilege role for election day tasks at the precinct.

The poll worker role allows a user to manage the polls on the precinct equipment, VxScan and VxMark. On both devices, the poll worker card is used to open and close polls on election day. On VxMark, the poll worker card is used to enable voter sessions. There are a few other actions enabled by the poll worker card - reprinting reports, powering down the machine, or checking the software hash - but overall the role is quite limited.

All poll worker cards are programmed at VxAdmin and are programmed for a specific election. They must be reprogrammed for every election. Poll worker cards may or may not require PINs depending on the value of `arePollWorkerCardPinsEnabled`  flag in the [system settings](election-package/#system-settings) file within the election package.

The poll worker role has no purpose on the central equipment, VxAdmin and VxCentralScan, and poll worker cards will be ignored on those devices.

## Election Manager Role

The election manager role is a broad role for election officials to setup and operate the election.

On the precinct equipment, an election manager card is used to configure the machines at the beginning of each election. This includes loading the election package, selecting a precinct for the device, and checking on consumables such as thermal paper for VxScan. At the end of an election, the election manager card can be used to unconfigure machines, re-export results, and export logs. In addition, system functions like setting date and time, turning on and off certain features, and accessing system diagnostics are available to election managers. The election manager card is not usually required at the precinct on election day, however, where the poll worker card should be sufficient for all election day tasks.

On the central equipment, an election manager card is used to access core election management features. On VxAdmin, it is used to load, adjudicate, review, and export results. On VxCentralScan, it is used to operate the scanner and export results.&#x20;

All election manager cards are programmed at VxAdmin and are programmed for a specific election. They must be reprogrammed for every election. They alway have PINs, which change after reprogramming the cards for a new election.

## System Administrator Role

The system administrator role is a powerful role for initial election setup and machine management. Unlike the poll worker and election manager roles, they are not tied to specific elections.

On VxAdmin, a system administrator card is necessary to initially load an election package from an external system. System administrators can then program poll worker cards and election manager cards for a specific election. In that sense, the system administrator role is the gatekeeper for loading elections and creating users, and is strictly necessary for every election.

On all devices, the system administrator role allows accessing a menu with powerful system actions. Many actions are shared with election managers - unconfiguring a machine or setting the date and time. Others are unique to the system administrator. For example, on precinct devices a system administrator can reset polls from a "closed" state to a "paused" state in case a poll worker accidentally closes polls prematurely.&#x20;

Additional system administrator cards can be programmed by a system administrator at VxAdmin. System administrator cards always have PINs. Because a system administrator card is necessary to program cards or set up elections to begin with, at least one pre-programmed card is initially provided with the voting system to bootstrap the jurisdiction's authentication.

## Vendor Role

The vendor role is a role that only VotingWorks itself has access to. It allows booting into an administrative menu with options to update various system configuration files.

## Voter Mode

While the authentication model only includes the four aforementioned roles, one can conceptually describe a "voter mode" on the precinct devices. On VxMark, a poll worker must authenticate in order to initiate a voting session. Once initiated, the voter is able to make selections, navigate menus, and print their ballot. Once done voting, the machine leaves voter mode and once again requires authentication to start a voting sesion. On VxScan, voter mode is any time the polls are open and no other role is authenticated, during which a ballot can be inserted for tabulation.

