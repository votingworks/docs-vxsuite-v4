# Hardware Criticality and Supplier Analysis

## Overview

VxSuite hardware contains hundreds of subcomponents, some of which are subassemblies containing hundreds or thousands of subcomponents themselves. Successfully building, deploying, and maintaining VxSuite requires that hundreds of components be sourced from scores of suppliers. If any component cannot be procured, it could impact the ability to build the system at all. If any component is defective or compromised, it could degrade the system's performance. In that sense, every component in a voting system is critical. Certain components are more critical than others, however, and the following analysis defines our strategy for ranking components with high, medium, or low criticality.

The two primary criteria we consider when assessing criticality are **ability to find alternative suppliers** and **relationship to sensitive election data**. If we are unable to easily find alternative suppliers, the component is at least medium criticality. If the component processes sensitive election data, the component is at least medium criticality. If both are true or one is especially true, the component is high criticality. In addition, there are a number of other lesser criteria mentioned below.

## Relationship to Sensitive Election Data

Any component that processes election data is at least medium criticality because, if it fails or is compromised by a malicious actor, it could theoretically alter configuration, operation, tabulation, or aggregation which could compromise the interpretation of ballots, election tallies, or voter privacy.

**Example 1:** Any scanner in the system, because it is responsible for recording ballot images, is a high criticality component. Defects in the scanner could produce unreliable ballot images. Sophisticated malicious attacks could alter firmware or intercept data transmission to produce altered images.

**Example 2:** USB cables transfer election data between components and are always at least medium criticality. USB cables are generally simple and replaceable, but highly sophisticated attacks involving manipulating data passing through a USB cable are possible.

**Example 3:** Power cables don't carry data to and from devices so, even though they are obviously critical to the operation of the device, they don't have a direct relationship to sensitive election data and are not more critical as a result.

## Ability to Find Alternative Suppliers

Most components can be or already are manufactured by multiple manufacturers. Standard screws can be purchased from various suppliers. Custom plastic or sheet metal components can be molded or cut by any number of manufacturers. Even power cables, simple USB cables, or something like a computer mouse can easily replace an equivalent.&#x20;

Some essential VxSuite components are unique to a single supplier or a small set of suppliers, however, making them at least medium criticality. When there is a single supplier, the product cannot be built as-designed without the support of that supplier. Additionally, a single supplier creates a direct supply chain attack vector.

**Example 1:** The embedded scanner in VxScan is manufactured and sold only by Peripheral Dynamics, Inc. Without being able to source the scanner from them, it would not be possible to build VxScan as is exists today, meaning the scanner high criticality.

**Example 2:** The case that forms the exterior of VxScan is a Pelican 1485 Air case. The product is designed around the case and, without the case, the product could not be built as-is, so the case is at least medium criticality. Conceivably, an alternative could be found, but it would not be straightforward.

**Example 3:** The anodized sheet metal panels that form the interior surfaces of VxScan can be cut and anodized by hundreds of metal shops across the country, so they are not more critical as a result of their supply.

## Other Considerations

### Ability to Quality Control

Any component can fail, but some component failures will be caught easily in quality control while others are more difficult to detect. For example, a misshapen sheet metal part will be caught in incoming parts QC or may result in the machine being not operable or not assemble-able. A slightly fraying cable, however, might perform adequately in QC but quickly deteriorate in performance. Components that are more complex, like a printer or cable, may exhibit deteriorated or even nefarious behavior that only manifests under certain conditions outside of QC.

Simple components where failure is easily detected are less critical than complex components where failure is more difficult to detect. Due to the complexity of a subassembly like an entire laptop, we're not able to effectively QC all of its many subsystems and have to rely on the supplier for their QC more than for a simple, transparent component.

### Physical Security

A seal point or hinge may be more critical than an interior panel because, if it is defective, it could break the physical security model of a device and allow someone to access a machine without tamper-evidence.

## Critical Components & Suppliers

In each article describing the hardware of a specific component, some section will specify the high and medium criticality components and provide some explanation of why it is deemed critical. All unlisted components are low criticality.

* [vxadmin-hardware.md](vxadmin-hardware.md "mention")















