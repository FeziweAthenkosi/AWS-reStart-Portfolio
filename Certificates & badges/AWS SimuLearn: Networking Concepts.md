# AWS SimuLearn: Networking Concepts – Portfoli

## Overview

This repository documents the practical implementations, architectural decisions, and diagnostic processes completed during the **AWS SimuLearn: Networking Concepts** learning experience. 

AWS SimuLearn utilizes generative AI-powered customer simulations alongside hands-on AWS console labs. The training focuses on gathering business requirements from virtual clients, translating those business needs into cloud architectures, and executing the technical deployment of secure, isolated network infrastructures on AWS.

---

## Skills Enhanced

Completing this simulation-driven course helped develop and refine competencies across several core cloud networking and communication areas:

### 1. Amazon VPC & Network Architecture
*   **Network Isolation:** Configured custom Virtual Private Clouds (VPCs) with public and private subnet structures to segregate logical layers.
*   **Internet Connectivity:** Attached and configured Internet Gateways (IGW) to facilitate external communication paths.
*   **Path Determination:** Formulated and validated custom Route Tables to control traffic flow from resources to the internet.

### 2. Network Security Controls
*   **Stateful Filtering:** Configured custom Security Groups to restrict and filter inbound and outbound traffic at the instance level.
*   **Security Group Referencing:** Implemented least-privilege security configurations by referencing web tier security groups directly inside database-tier security rules (rather than exposing database ports to broad IP ranges).

### 3. Network Diagnostics & Troubleshooting
*   **Isolation Analysis:** Traced pathing failures, misconfigured route associations, and missing or overly restrictive Security Group rules.
*   **Consolidated Remediation:** Reviewed active VPC configurations systematically in a live AWS environment to identify and resolve connectivity blockages.

---

## Simulated Business Scenario & Hand-on Labs

The practical application of these skills was verified in a simulated business scenario involving a financial institution:

### 🏦 Scenario: Secure Banking Network Design
*   **Client Need:** A financial institution required a secure network architecture to manage communication between private database servers, public web endpoints, and external banking services.
*   **Simulation phase:** Interacted with virtual clients to confirm security and compliance requirements.
*   **Deployment phase:** Constructed the cloud infrastructure in a live-provisioned AWS Console environment.
*   **Troubleshooting phase:** Diagnosed a multi-tier connectivity issue within the VPC, successfully restoring secure public and private reachability without compromising security standards.

---

## AWS Services Utilized

*   **Amazon VPC** (Virtual Private Cloud)
*   **Internet Gateway (IGW)**
*   **Route Tables & Associations**
*   **Security Groups**
*   **Amazon EC2**


<img width="1126" height="842" alt="aws_simulearn_networking" src="https://github.com/user-attachments/assets/c803d1c4-b741-48d5-a79f-a40e9902b7d3" />

The completion certificate and metadata for this credential can be verified through the AWS Skill Builder platform:
*   **Learning Platform:** [AWS Skill Builder](https://explore.skillbuilder.aws/)
*   **Course Details:** AWS SimuLearn: Networking Concepts
