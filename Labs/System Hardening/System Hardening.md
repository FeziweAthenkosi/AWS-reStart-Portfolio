# Systems Hardening with Patch Manager via AWS Systems Manager

In this project, I configured and executed OS patch management for a hybrid-like fleet of EC2 instances (three Linux and three Windows nodes) using **AWS Systems Manager (SSM) Patch Manager**. 

Below is a detailed walkthrough of the implementation steps, explaining the actions taken and how they were verified using the AWS Management Console.

---

## Task 1: Patching Linux Instances with Default Baselines

### 1. Verifying Managed Nodes in Fleet Manager
To start, I navigated to **Systems Manager > Fleet Manager** to verify that all the pre-created instances were properly registered and online. I observed three Linux instances online: `Linux-1`, `Linux-2`, and `Linux-3`.

![Managed Nodes in Fleet Manager](images/fleet_manager_nodes.png)
*Fleet Manager displaying the active Linux managed nodes.*

I selected the `Linux-1` node (`i-06933cdf55568358a`) and reviewed its details. I confirmed it was running Amazon Linux 2 and verified that the necessary IAM instance profile (`arn:aws:iam::964150127062:instance-profile/RoleForSSM`) was attached, allowing Systems Manager to communicate with the instance.

![Linux Instance Details](images/linux_node_details.png)
*Reviewing the SSM configuration and platform details of Linux-1.*

---

### 2. Identifying the Default Linux Patch Baseline
Next, I opened **Patch Manager** and selected the **Patch baselines** tab. I located the predefined default patch baseline for Amazon Linux 2, which is named `AWS-AmazonLinux2DefaultPatchBaseline` (ID: `pb-0e930e75b392d7da`). This baseline governs how security and critical updates are approved and applied to Amazon Linux 2 nodes.

![Patch Baselines Tab](images/default_patch_baselines.png)
*Default patch baselines listing with AWS-AmazonLinux2DefaultPatchBaseline highlighted.*

---

### 3. Configuring and Initiating the Patch Now Operation
To patch the Linux instances, I initiated an on-demand patch operation using **Patch now**. I configured the settings as follows:
* **Patching operation:** Scan and install
* **Reboot option:** Do not reboot my instances
* **Instances to patch:** Patch only the target instances I specify (targeted via Instance Tags)
* **Target selection:** Tag key: `Patch Group` | Tag value: `LinuxProd`

![Patch Now Configuration](images/patch_now_config.png)
*Patch now configuration screen targeting the LinuxProd patch group.*

---

### 4. Monitoring the Patch Execution
After selecting **Patch now**, the task executed via State Manager. I monitored the **Association execution summary** page, which confirmed that the process ran successfully and applied updates to all three targeted Linux instances (`Success=3`).

![Linux Patch Execution Summary](images/linux_patch_success.png)
*Successful association execution summary for the LinuxProd patch group.*

---

## Task 2: Creating a Custom Patch Baseline for Windows Instances

To apply controlled security updates to the Windows Server 2019 instances, I created a custom patch baseline instead of using the default baseline.

### 1. Creating the Custom Baseline
I navigated back to **Patch Manager > Patch baselines** and selected **Create patch baseline**. I configured the baseline details as follows:
* **Name:** `WindowsServerSecurityUpdates`
* **Description:** `Windows security baseline patch`
* **Operating system:** Windows
* **Approval Rules:** 
  * **Rule 1:** Target product `WindowsServer2019` with a severity of `Critical` and classification of `SecurityUpdates` with an auto-approval period of 3 days.
  * **Rule 2:** Target product `WindowsServer2019` with a severity of `Important` and classification of `SecurityUpdates` with an auto-approval period of 3 days.

Upon creation, the total number of baselines updated to 18.

![Create Baseline Success](images/custom_baseline_success.png)
*Patch baselines dashboard showing the creation confirmation banner.*

---

### 2. Associating the Custom Baseline with a Patch Group
To ensure my Windows instances would automatically use this baseline during run executions, I selected my newly created baseline (`WindowsServerSecurityUpdates` / `pb-099ae86c3b74aad43`), clicked **Actions > Modify patch groups**, and added the patch group named `WindowsProd`.

![Modify Patch Groups](images/add_patch_group.png)
*Associating the WindowsProd patch group with the custom Windows baseline.*

---

## Task 3: Patching the Windows Instances

### 1. Tagging the Windows EC2 Instances
Before executing the baseline, I needed to make sure the target instances belonged to the matching patch group. I went to the **EC2 console > Instances** and selected `Windows-1` (`i-0e15d988011d75e6e`). I accessed the **Tags** tab and added the following tag:
* **Key:** `Patch Group`
* **Value:** `WindowsProd`

I then repeated this process for the `Windows-2` and `Windows-3` instances so they were all grouped identically.

![Manage EC2 Tags](images/tagging_windows.png)
*Assigning the Patch Group tag to the Windows-1 instance.*

---

### 2. Running Patch Now for Windows
With the instances tagged, I returned to **Patch Manager** and selected **Patch now**. I configured it to run a **Scan and install** operation, targeted the tag key `Patch Group` with the value `WindowsProd`, and set it to not reboot the instances. 

The execution details page confirmed that the operation completed successfully across all 3 Windows instances.

![Windows Patch Execution Summary](images/windows_patch_success.png)
*Successful execution summary for the WindowsProd group.*

---

## Verification and Compliance Summary

By completing these actions, I verified that:
1. Both Linux and Windows instance groups were targeted using SSM patch groups.
2. The default baselines were applied to the Amazon Linux instances.
3. A custom-tailored security patch baseline was associated and executed against the Windows Server 2019 fleet.
4. Compliance reporting confirmed that all six managed nodes reached the required baseline configuration.
