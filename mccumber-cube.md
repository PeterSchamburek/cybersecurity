# The McCumber Cube: A Worked Example

The McCumber Cube (also known as the CNSS Security Model) is a framework for analyzing information security across three dimensions:

- **Security Properties**: Confidentiality, Integrity, Availability
- **Information States**: Storage, Processing, Transmission
- **Safeguards**: Policy, Education (People), Technology

Below is a worked example mapping a specific safeguard to each of the 27 intersections.

## Confidentiality

| State | Policy | Education | Technology |
|---|---|---|---|
| **Storage** | Implement policy regarding data retention and disposal based on a data classification scheme. | Train employees on the proper disposal of company data and hard drives. | Implement Full Disk Encryption (FDE) on company computers. |
| **Processing** | Implement policy requiring employees keep phones out of work spaces while data is being processed, preventing eavesdropping via compromised devices and reducing insider threat risk. | Train employees to identify dangerous apps or websites to avoid when processing company data. | Utilize homomorphic encryption when computing with company data. |
| **Transmission** | Implement policy dictating what mediums various classifications of data may be transmitted by (e.g., no company secrets over SMS). | Train employees on safe handling of company computers and drives when moving between locations. | Utilize VPNs when transmitting data across the internet. |

## Integrity

| State | Policy | Education | Technology |
|---|---|---|---|
| **Storage** | Implement policy mandating the use of hash functions to verify the integrity of stored data. | Train employees to periodically review saved files to ensure integrity. | Run CHKDSK (Windows) / fsck (Linux) regularly to detect and repair file system corruption. |
| **Processing** | Implement policy requiring database systems to maintain ACID compliance for all transactions. | Train employees to double-check and verify with others prior to saving or uploading data. | Utilize ECC memory to detect and correct bit errors in data while actively processed in RAM. |
| **Transmission** | Implement policy requiring company websites use HTTPS over HTTP. | Train employees to verify downloads with hash values. | Utilize TCP rather than UDP for transmitting packets related to company data and operations. |

## Availability

| State | Policy | Education | Technology |
|---|---|---|---|
| **Storage** | Implement a data backup and disaster recovery policy to ensure stored data can be restored if lost. | Train employees to make copies of stored files to preserve availability. | Utilize RAID 5, 6, or 10 to ensure data availability. |
| **Processing** | Implement Recovery Time Objective (RTO) and Recovery Point Objective (RPO) targets to maintain processing continuity during adverse events. | Train employees not to force-quit active work applications, to avoid interrupting running processes. | Employ Uninterruptible Power Supplies (UPS) to protect processing systems against blackouts or brownouts. |
| **Transmission** | Implement Service Level Agreement (SLA) terms guaranteeing minimal network downtime. | Train employees not to use unauthorized network devices that could interrupt network traffic. | Utilize Spanning Tree Protocol (STP) on company networks. |

---
*A study reference built while working through the CNSS/McCumber Cube model.*
