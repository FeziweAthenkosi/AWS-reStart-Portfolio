# AWS EC2 Setup Lab: Deploying and Managing a Web Server

This repository documents the step-by-step process of launching, configuring, scaling, and terminating an Amazon Elastic Compute Cloud (EC2) instance. The lab demonstrates how to deploy a basic web server using automation scripts and configure network security settings to expose the server to the public internet.

---

## Lab Objective
To gain hands-on experience provisioning and managing virtual servers in the AWS cloud environment. This includes configuring security groups (firewalls), writing startup (User Data) scripts to automate software installations, scaling hardware specs dynamically, and practicing safe resource deletion.

---

## Step-by-Step Implementation

### Phase 1: Accessing the AWS Management Console
1. Log in to the AWS Management Console.
2. In the top search bar, search for and select **EC2** to open the EC2 Dashboard.

![AWS Console Dashboard](images/01-aws-console.png)

---

### Phase 2: Launching the EC2 "Web Server"
1. On the EC2 Dashboard, click **Launch instance**.
2. Configure the following settings:
   * **Name:** `Web Server`
   * **Application and OS Image (AMI):** Select the default **Amazon Linux** AMI.
   * **Instance type:** Select **t2.micro** (or `t3.micro` depending on region availability).
   * **Key pair:** Select **Proceed without a key pair** (since we are using automated script deployment instead of direct SSH).

![Instance Configuration](images/02-instance-config.png)

3. **Network Settings:**
   * Select **Create security group**.
   * Set the Security group name to `Web Server security group`.
   * Ensure only default settings are used, and do not allow HTTP traffic yet.

![Security Group Setup](images/03-network-settings.png)

4. **Advanced Details:**
   * Scroll down to **Termination protection** and set it to **Enable**.
   * Scroll to the very bottom to the **User data** text box and paste the following bash script to automate the installation of an Apache web server:
