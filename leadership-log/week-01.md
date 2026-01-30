## Leaderhip Reflection Log Week 1

### Name: Niharika Kalkeri
### Week 1

### Project: Designing and Securing a Production-Ready AWS Environment Using Least Privilege, Network Isolation, and Threat Detection
### Focus Area: AWS Cloud Security Architecture
### Timeframe: 1/25/26-2/1/26


### Week Overview

This week, I designed and implemented a production-ready AWS security architecture focused on least privilege, network isolation, and continuous threat detection. The environment was intentionally built to eliminate public exposure while maintaining operational functionality through private networking and controlled outbound access. I implemented identity, network, data, and detection controls aligned with real-world cloud security best practices. The primary outcome was a secure-by-default AWS environment with full auditability and cost-abuse visibility.


### Ownership

#### What did I take full responsibility for this week?

* Took full ownership of the end-to-end security design, not just resource deployment.
* Defined security requirements before provisioning infrastructure.
* Treated the environment as production-facing rather than a sandbox.

#### Specific ownership actions:

* Designed IAM roles with service-specific least-privilege policies instead of reusing broad permissions.
* Ensured no long-term credentials existed for workloads.
* Verified root account security (MFA) and enforced preventive controls rather than relying on detection alone.


### Curiosity

#### Key questions I asked during this lab:

* What would a real attacker try first in a misconfigured AWS account?
* Which misconfigurations are most likely to lead to data exposure or cost abuse?
* How can I detect security failures even if prevention controls fail?
* What signals would a SOC realistically rely on in AWS?

#### Actions driven by curiosity:

* Enabled GuardDuty to understand baseline vs suspicious behavior.
* Used AWS Config rules to validate that controls remained enforced over time.
* Thought through cost-abuse scenarios and implemented budget alarms proactively.


### Delivery

#### Security architecture delivered:

#### Identity

* IAM roles used exclusively for services
* One role per service with scoped permissions
* Root account protected with MFA
* No IAM users or long-term access keys

#### Network

* VPC with public subnet limited to NAT Gateway only
* All workloads deployed in private subnets
* No public EC2 instances
* Security groups tightly scoped to required traffic only

#### Data
* S3 bucket fully private with Block Public Access enabled
* Server-side encryption enforced using KMS
* Access logging enabled for auditability

#### Detection & Monitoring

* CloudTrail enabled and centralized in S3
* GuardDuty activated for continuous threat detection
* AWS Config rule to detect public S3 exposure
* Budget alarms configured to detect abnormal cost spikes


### Challenges & Trade-offs

#### Key challenges:

* Designing least-privilege IAM policies without breaking service functionality.
* Balancing strict network isolation with required outbound access.
* Understanding which detections provide signal vs noise.

#### How I handled them:

* Iteratively refined IAM policies based on actual service needs.
* Used NAT instead of public access to preserve isolation.
* Chose detections that map to high-impact failure scenarios rather than enabling everything.

### Lessons Learned

#### Key takeaways:

* Most cloud breaches start with identity misconfigurations, not exploits.
* Preventive controls reduce risk, but detection validates trust.
* Cost abuse is a security problem, not just a finance issue.

#### What I’ll improve next iteration:

* Add alert correlation between CloudTrail and GuardDuty findings.
* Expand Config rules to cover IAM policy drift.
* Simulate misconfigurations to validate detection effectiveness.

### Final Reflection:
This project reinforced my mindset shift from “deploying AWS services” to engineering secure cloud systems with ownership and accountability.
