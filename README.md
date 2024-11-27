# docs-vxsuite-v4

## Repository Structure
- `conformity-matrix/` contains a matrix of each VVSG2 requirement with a brief description of how VxSuite meets the requirement, how VotingWorks tests meeting the requirement, and a reference to where to find more documentation supporting this requirement in the Technical Data Package (TDP).
- `docs-vxsuite-v4-tdp` is a submodule that syncs the content of the VxSuite TDP that is publicly avialable at: https://docs.voting.works/vxsuite-tdp-v4
- `docs-vxsuite-v4-user-manual` is a submodule the content of the VxSuite User Manual that is publicly available at: https://docs.voting.works/vxsuite-user-manual-v4
- `hardware-assets/`
  - `BOMs/` contains the detailed Bill of Materials for each component in the system
  - `cots-documentation/` contains all of the data sheets for COTS products used in the system
  - `drawings/` contains all of the mechanical drawings for manufactured parts in the system
  - `workplans/` contains detailed instructions for assembling the system
- `quality-assurance/` contains documents used in VotingWorks internal QA
  - `testing` contains test results for the system performed by either external bodies or by VotingWorks
- `risk-assessment/` contains a risk assessment for the voting system per VVSG 14.1
- `uat-reports/` contains the voter and poll worker reports from usability and accessibility testing
- `warranty-model/` contains a copy of the VotingWorks service contract

## Downloading Documentation

Documentation available at docs.voting.works is available for PDF download on the website by clicking `Export as PDF`. Click `All pages` for the entirety of the documentation. For ease of navigation, a search feature is also available for these hosted documents by clicking `Ask or search` or `ctrl-K` when viewing the documentation. You can search for a given section of the documentation or ask a question in natural language and receive an AI summarized answer based on the documentation content.

The files in this repository are available for download as a .zip file by clicking `Code` > `Download Zip`. Submodules are available for download in the same manner from their respective linked repositories.

## Code Repositories

There are four code repositories relevant to the voting system that this respository documents:

- [vxsuite](https://github.com/votingworks/vxsuite/tree/v4.0.0-release-branch) — Core application code
- [kiosk-browser](https://github.com/votingworks/kiosk-browser/tree/v4.0.0-release-branch) — Generic Electron-based kiosk-mode browser
- [vxsuite-complete-system](https://github.com/votingworks/vxsuite-complete-system/tree/v4.0.0-rc2) — Links compatible versions of vxsuite and kiosk-browser, and includes the scripts necessary to create a production machine
- [vxsuite-build-system](https://github.com/votingworks/vxsuite-build-system/tree/v4.0.0) — Our framework for building VxSuite and managing its dependencies, across versions and environments

Separate from the above is [vx-iso](https://github.com/votingworks/vx-iso), our VotingWorks-specific ISO installer program.
