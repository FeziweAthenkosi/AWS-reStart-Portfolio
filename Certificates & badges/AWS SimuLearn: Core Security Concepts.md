# AWS SimuLearn: Core Security Concepts

This repository documents the completion of the **AWS SimuLearn: Core Security Concepts** hands-on learning simulation. This training focuses on fundamental cloud security practices, specifically implementing identity and access management controls to secure AWS resources.

---

## Scenario Overview

In this simulation, a financial institution (stock exchange) required enhanced security controls to restrict their support engineers' access. The objective was to configure permissions so that engineers could only perform the actions necessary for their specific role, aligning with cloud security best practices.

### Objectives & Technical Steps
1. **Create an IAM Group:** Form a dedicated group specifically for support engineers to streamline permission management.
2. **Apply Least Privilege Access:** Attach managed read-only policies to the IAM group to grant visibility without modify permissions:
   * `AmazonEC2ReadOnlyAccess` (for compute resources)
   * `AmazonRDSReadOnlyAccess` (for database resources)

---

## AWS Services Used

* **AWS Identity and Access Management (IAM):** Used to securely manage access to AWS services and resources. 
  * *IAM Groups:* Created to organize users with similar job functions.
  * *IAM Policies:* Utilized to define permissions (specifically AWS managed read-only policies).
* **Amazon Elastic Compute Cloud (Amazon EC2):** Configured and restricted read-only permissions for virtual servers.
* **Amazon Relational Database Service (Amazon RDS):** Applied read-only permissions to ensure secure, read-only visibility into database infrastructure.

---

## Skills Enhanced

* **Principle of Least Privilege (PoLP):** Practiced the foundational security practice of granting users only the minimum levels of access necessary to complete their job tasks.
* **Role-Based Access Control (RBAC):** Grouped users based on their job roles and assigned permissions to the group rather than to individual identities, simplifying administration and reducing the risk of permission creep.
* **AWS Policy Management:** Gained practical understanding of utilizing AWS-managed policies (such as `AmazonEC2ReadOnlyAccess` and `AmazonRDSReadOnlyAccess`) to securely delegate read-only access across multiple core AWS services.<img width="1091" height="775" alt="Screenshot 2026-06-21 205436" src="https://github.com/user-attachments/assets/db37f053-d4f4-403d-b02e-9fbf29979cb7" />
