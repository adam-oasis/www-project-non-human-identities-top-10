# NHI1:2025 Improper Offboarding

| Threat Agents & Attack Vectors                    | Security Weakness                                                                                          | Impact                                         |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| Exploitability: **Easy**            | Prevalence: **Widespread**<br>Detectability: **Hard**                       | Technical: **Severe**<br>Business: **Specific**     |
| Exploiting an improperly offboarded NHI greatly depends on context. Considering the case of an inside threat or lateral movement, it’s quite simple to identify what necessary credentials are needed to exploit the improperly offboarded identity. | The current capabilities of offboarding NHIs, such as service accounts, are lackluster, and organizations rarely use existing possibilities. Thus, many NHIs are not properly offboarded after they are no longer needed or once the original owner has left.<br>Security teams are lacking tools to detect old NHIs that are no longer used and were not properly offboarded. Existing techniques of detecting such NHIs rely on incomplete information that takes a long time to compile.      | Due to the deep insight a potential inside threat has of the organization, exploiting improperly offboarded NHIs could lead to compromise of critical systems, exfiltration of sensitive data and usage of advanced persistence methods. |

## Description
Improper offboarding refers to the inadequate deactivation or removal of non-human identities (NHIs) such as service accounts and access keys when they are no longer needed. This situation typically arises due to one of the following scenarios:
1. When applications are deprecated or services are taken offline, rendering the NHIs they depended on unneeded and unused (commonly referred to as "stale" or "dormant").
2. When the original owner of the NHIs leaves the organization, but the identities are still in use without an active owner (commonly referred to as "orphaned").
3. When an administrator or developer who is often _not_ the NHI owner is exposed to their credentials, and leaves the organization without revoking said credentials (commonly referred to as "partially offboarded employee").

The failure to properly offboard NHIs poses significant security risks. Unmonitored and deprecated services may remain vulnerable, and their associated NHIs can be exploited by attackers to gain unauthorized access to sensitive systems and data. Additionally, such NHIs may retain elevated permissions, amplifying the potential damage from any security breach.

## Example Attack Scenarios
- **Dormant Kubernetes Service Accounts:** A Kubernetes cluster belonging to a decommissioned service retains active service accounts. If an attacker gains access to this unmonitored cluster, they could exploit these service accounts to interact with other resources within the organization's infrastructure, potentially leading to data exfiltration or further compromise.
- **Leftover Apps Used for Privilege Escalation & Lateral Movement:** An application is created in a non-production environment in order to test a workload. As part of the testing suite, it is connected to a sensitive environment. The application is not decommissioned even once the workload is transferred to run in a production server. Then, an attack reaching the less secure non-production environment can use this application to move laterally within the organization.
- **Ex-Employee Exploiting Unrevoked Credentials:** An employee who managed automated services and was exposed to credentials leaves the organization, but the NHIs associated with those credentials are not revoked or rotated. The ex-employee could misuse still-valid credentials to access the organization's systems remotely, even if his personal account was revoked, leading to unauthorized data access, service disruptions, or even sabotage.
- **Employee leaves, but the account remains:** A skilled application developer who built a business-critical application years ago, decides to move on. Application ownership is moved to a new team, but no one in the organization has full context on how the application works, and the fact that it leverages an access key for operation is forgotten. As time passes, the existence of the key goes unnoticed and remains active, creating a security vulnerability.  

## How to Prevent
- Implement an offboarding process that reviews all NHIs associated with departing employees. Determine if associated NHI are still required - if not, decommission them; otherwise, transfer ownership to another employee and rotate any credentials the departing employee may have had access to during its lifecycle.
- Automate offboarding steps wherever possible by integrating HR systems with identity and access management (IAM) tools.
- Regularly recertify NHIs, to confirm they are still in use, actively needed, and have valid owners. Decomission any identities no longer needed, and ensure all NHIs have owners.
- Regularly audit active NHIs to identify ongoing usage and block potential misuse.

## References
- [Oasis Security: Decommissioning Orphaned and Stale Non-Human Identities](https://www.oasis.security/resources/blog/decommissioning-orphaned-and-stale-non-human-identities)
- [Ex-Employee Accessed Former Company's System and Deleted Resources](https://www.channelnewsasia.com/singapore/former-employee-hack-ncs-delete-virtual-servers-quality-testing-4402141)
- [Microsoft Breach by Midnight Blizzard Threat Actor](https://msrc.microsoft.com/blog/2024/01/microsoft-actions-following-attack-by-nation-state-actor-midnight-blizzard/)

## Data Points
- CSA NHI Report - 31% answers put insufficient NHI offboarding as one of the top 3 most concerning NHI threats. (5/10)
- CSA NHI Report - 32% of times orphaned identities were the cause for NHI-related security incidents. (4/10)
- CSA NHI Report - 15% of organizations need automated provisioning and de-provisioning as the most important capability of an NHI tool. (9/16)
- CSA NHI Report - 51% of organizations have no formal process to offboard or revoke long lived API keys.
- Recent Breach - [Microsoft Breach](https://medium.com/@ronilichtman/how-to-protect-yourself-from-the-microsoft-oauth-attack-powershell-scripts-included-71b398034b8d)
