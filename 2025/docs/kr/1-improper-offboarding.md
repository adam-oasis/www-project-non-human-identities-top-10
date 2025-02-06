# NHI1:2025 Improper Offboarding

| Threat Agents & Attack Vectors                    | Security Weakness                                                                                          | Impact                                         |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| Exploitability: **Easy**            | Prevalence: **Widespread**<br>Detectability: **Hard**                       | Technical: **Severe**<br>Business: **Specific**     |
| 부적절하게 오프보딩된 NHI를 악용하는 것은 상황에 따라 다릅니다. 다만, 내부 위협 시나리오를 생각하면, 부적절하게 오프보딩된 ID를 찾아내고, 악용하는건 쉽고, 파급도가 높은 해킹경로로 사용될 수 있습니다. | 서비스 계정이나 API 키와 같은 NHI(Non-Human Identities)의 오프보딩 기능을 제공하는 플랫폼은 적으며, 해당 기능을 활용하는 조직은 많지 않습니다. 따라서 많은 NHI가 사용되지 않거나, 접근 가능한 사용자가 변경된 이후에도 같은 권한을 유지하고, 적절하게 오프보딩 되지 않습니다. <br> 보안팀은 적절하게 오프보딩되지 않은 오래된 NHI(Non-Human Identities)를 탐지할 도구가 부족하고, 불완전한 정보에 의존하고 있으며 정보를 취합하는데 있어 오랜 시간이 걸립니다.  | 부적절하게 오프보딩 된 NHI를 부적절한 내부자 또는 공격자가 접근하게 될 경우, 중요한 시스템의 손상, 민감한 데이터의 유출 및 지속적인 해킹 경로로 이용될 수 있습니다. |

## Description
부적절한 오프보딩은 더 이상 필요하지 않은 서비스 계정 및 액세스 키와 같은 Non-Human Identities(NHI)의 불충분한 비활성화 또는 불충분한 제거를 의미합니다. 이러한 상황은 가플리케이션이 더 이상 사용되지 않거나, 서비스가 오프라인으로 전환되거나, 해당 NHI의 원래 소유자 또는 관리자가 조직을 떠날 때 발생합니다. NHI를 적절하게 오프보딩하지 못하면 심각한 보안 위험이 발생합니다. 모니터링되지 않고 더 이상 사용되지 않는 서비스는 취약한 상태로 남아 있을 수 있으며, 관련 NHI는 공격자가 악용하여 민감한 시스템 및 데이터에 대한 무단 액세스 권한을 얻을 수 있습니다. 또한, 방치된 NHI는 상승된 권한을 유지할 수 있으며, 이는 보안 침해로 인한 잠재적 피해를 증폭시킵니다.

## Example Attack Scenarios
- **방치된 Kubernetes 서비스 계정:** 더 이상 사용되지 않는 서비스에 속한 Kubernetes 클러스터는 활성화된 서비스 계정을 유지하고 있습니다. 만약 공격자가 이 모니터링되지 않는 클러스터에 접근 권한을 얻게 된다면, 이 서비스 계정들을 악용하여 조직의 인프라 내 다른 자원들과 상호작용할 수 있으며, 이는 잠재적으로 데이터 유출이나 추가적인 침해로 이어질 수 있습니다.
- **비활성화 되지 않은  자격증명을 악용하는 퇴사자:** 자동화된 서비스를 관리하던 직원이 퇴사했지만, 해당 서비스와 연결된 Non-Human Identities(NHI)는 비활성화되거나 변경되지 않았습니다. 퇴사자는 여전히 유효한 자격 증명을 오용하여 조직 시스템에 원격으로 액세스할 수 있으며, 이는 무단 데이터 접근, 서비스 중단, 심지어는 사보타주로 이어질 수 있습니다는
- **측면 이동 또는 권한상승에 악용되는 어플리케이션:** 테스트 환경에서 워크로드를 테스트하기 위해 생성된 애플리케이션이 나중에 테스트를 완료하기 위해 민감한 운영 환경에 연결되고, 해당 워크로드가 운영 서버에서 실행되도록 이전된 후에도 폐기되지 않았습니다. 상대적으로 보안수준이 낮은 테스트 환경에 접근한 공격자가 해당 애플리케이션을 사용하여 조직 내에서 측면으로 이동할 수 있고, 공격에 악용될 수 있습니다.
당
## How to Preven한
- 퇴사하는 직원과 연결된 모든 NHI를 검토하는 오프보딩 프로세스를 구현합니다. 각 NHI에 대해 여전히 필요한지 확인합니다. 필요하지 않은 경우 폐기하고, 그렇지 않은 경우 소유권을 다른 직원에게 이전하고 퇴사하는 직원이 생성 중에 액세스했을 수 있는 모든 자격 증명을 교체합니다.
- 인사 시스템과 ID 및 접근 관리(IAM) 도구를 통합하여 가능한 모든 곳에서 오프보딩 단계를 자동화합니다.
- 활성 NHI에 대한 감사를 수행하고, 지속적으로 사용하는지 확인하며 잠재적인 위협을 차단합니다.

## References
- [Cloud Security Alliance: Decommissioning Orphaned and Stale Non-Human Identities](https://cloudsecurityalliance.org/blog/2024/06/03/decommissioning-orphaned-and-stale-non-human-identities)
- [Ex-Employee Accessed Former Company's System and Deleted Resources](https://www.channelnewsasia.com/singapore/former-employee-hack-ncs-delete-virtual-servers-quality-testing-4402141)
- [Microsoft Breach by Midnight Blizzard Threat Actor](https://msrc.microsoft.com/blog/2024/01/microsoft-actions-following-attack-by-nation-state-actor-midnight-blizzard/)

## Data Points
- CSA NHI Report - 31%의 응답자가 불충분한 NHI 오프보딩을 가장 우려되는 상위 3가지 NHI 위협 중 하나로 꼽았습니다. (5/10)
- CSA NHI Report - NHI 관련 보안 사고의 32%는 방치된 ID가 원인이었습니다. (4/10)
- CSA NHI Report - 15%의 조직은 자동화된 프로비저닝 및 디프로비저닝을 NHI 도구의 가장 중요한 기능으로 필요로 합니다. (9/16)
- CSA NHI Report - 51%의 조직은 수명이 긴 API 키를 오프보딩하거나 폐기하는 공식적인 절차가 없습니다.
- 최근 유출 사고  - [Microsoft Breach](https://medium.com/@ronilichtman/how-to-protect-yourself-from-the-microsoft-oauth-attack-powershell-scripts-included-71b398034b8d)
