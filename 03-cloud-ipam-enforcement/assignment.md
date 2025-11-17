---
slug: cloud-ipam-enforcement
id: mfeh7kamxx8b
type: challenge
title: ' Enforce IPAM Policies in the Cloud'
teaser: UDDI-Driven AWS VPC Deployment + Enforcement
notes:
- type: video
  url: https://videos.infoblox.com/watch/oV53DGRkS6SNtsmiyeg4Sh?
tabs:
- id: fgtdtxedh0gt
  title: Shell
  type: terminal
  hostname: shell
- id: a9bnefa5cmik
  title: Editor
  type: code
  hostname: shell
  path: /root/infoblox-lab
- id: nb7efktl9ago
  title: AWS Console
  type: browser
  hostname: aws
- id: myjvsylzmmry
  title: Azure Console
  type: browser
  hostname: azure
- id: mtpaekaicgjl
  title: GCP Console
  type: browser
  hostname: gcp
- id: bj2vx4uycy59
  title: Infoblox Portal
  type: browser
  hostname: infoblox
- id: 42pehxtfmkvt
  title: Lab Diagram
  type: browser
  hostname: lab
difficulty: ""
timelimit: 0
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---
🚀 UDDI-Driven AWS VPC Deployment + Enforcement Demo (Terraform)

🧭 Description

In this hands-on lab, you’ll demonstrate how Infoblox Universal DDI (UDDI) provides a centralized, authoritative control plane for managing IP allocations across AWS using Terraform.

You will:
- Dynamically pull IP space from UDDI
- Deploy AWS VPC/Subnet using this space
- Attempt to reuse the same IP block and watch UDDI deny it
- Simulate external misuse and show why Terraform + UDDI is safer


## 1) Login to your cloud account consoles
===

🔐 (Optional) Log in to Your Cloud Account Consoles

You should already be signed in to both the AWS,Azure and GCP web consoles via the embedded tabs on the left-hand side of the Instruqt interface.

⚠️ Only perform this step if you’re logged out or the session has expired.

- Use the credentials provided in the lab instructions to sign in.
- Skip any onboarding wizards or tutorials (especially on Azure).
- If prompted for account type on AWS, select IAM Account.
---
# AWS Credentials ☁️

Select "IAM Account" and enter the **AWS ID**:
```
[[ Instruqt-Var key="INSTRUQT_AWS_ACCOUNT_INFOBLOX_DEMO_ACCOUNT_ID" hostname="shell" ]]
```

**AWS Username**
```
[[ Instruqt-Var key="INSTRUQT_AWS_ACCOUNT_INFOBLOX_DEMO_USERNAME" hostname="shell" ]]
```

**AWS Password**
```
[[ Instruqt-Var key="INSTRUQT_AWS_ACCOUNT_INFOBLOX_DEMO_PASSWORD" hostname="shell" ]]
```

---

# AZURE Credentials ☁️

**AZURE SUBSCRIPTION**
```
[[ Instruqt-Var key="INSTRUQT_AZURE_SUBSCRIPTION_INFOBLOX_TENANT_SUBSCRIPTION_ID" hostname="shell" ]]
```

**AZURE Username**
```
[[ Instruqt-Var key="INSTRUQT_AZURE_SUBSCRIPTION_INFOBLOX_TENANT_USERNAME" hostname="shell" ]]
```

**AZURE Password**
```
[[ Instruqt-Var key="INSTRUQT_AZURE_SUBSCRIPTION_INFOBLOX_TENANT_PASSWORD" hostname="shell" ]]
```
---

# GCP Credentials ☁️

**GCP Project**
```
[[ Instruqt-Var key="INSTRUQT_GCP_PROJECT_INFOBLOX_DEMO_PROJECT_NAME" hostname="shell" ]]
```

**GCP Username**
```
[[ Instruqt-Var key="INSTRUQT_GCP_PROJECT_INFOBLOX_DEMO_USER_EMAIL" hostname="shell" ]]
```

**GCP Password**
```
[[ Instruqt-Var key="INSTRUQT_GCP_PROJECT_INFOBLOX_DEMO_USER_PASSWORD" hostname="shell" ]]
```
---


🧱1️⃣ Create a VPC using IP details  from Infoblox IPAM
==


We’ll use Infrastructure as Code (IaC) with Terraform to provision resources, integrating both the AWS and Infoblox providers to source data directly within the main Terraform code.


🔧 Step-by-step:
	1.	First, initialize Terraform in the terminal using:

```run
cd ~/infoblox-lab/uddi-ipam/terraform/ipam-test/
terraform init
```


2.	Then, apply the configuration:

```run
cd ~/infoblox-lab/uddi-ipam/terraform/ipam-test/
terraform apply --auto-approve
```

![Screenshot 2025-07-11 at 11.22.42.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/de54fe5d4d79b02cf01966bc229d4671/assets/Screenshot%202025-07-11%20at%2011.22.42.png)

This will provision the AWS resources using IP address data managed in Infoblox UDDI.


> [!IMPORTANT]
> Note that the actual subnet_id and vpc_id values in your environment will differ from the sample output shown above.

🧠 Pro tip:
To review or edit the Terraform code, use the Editor tab located in the left-hand panel of the Instruqt lab environment.


 ✅ Key Demo Ideas: Enforcing and Reusing IP Blocks with UDDI


## 1️⃣ Review Existing On-Prem IPAM with Federated Realms

✅ Steps:
1.	Log into the Infoblox UDDI Web Console.
2.	From the left-hand menu, go to Configure → Networking → IPAM Realms.
3.	Select the ACME Corporation Federated Realm.
4.	Inspect how top-level blocks are structured (AWS, Azure, GCP).
5.	Dive deeper into the delegated block 10.20.0.0/16 and its child block 10.20.20.0/24.

🔍 Screenshot Walkthrough

👉 Step 1: Navigate to IPAM Realms

![Screenshot 2025-07-11 at 07.45.01.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/380dd567f7bad3e7309e2c62c25967cd/assets/Screenshot%202025-07-11%20at%2007.45.01.png)

👉 Step 2: Locate the Federated Realm (ACME Corporation)

![Screenshot 2025-07-11 at 07.45.09.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/060b79dbd1b9e95b3d4b2c88efd2b9c4/assets/Screenshot%202025-07-11%20at%2007.45.09.png)

👉 Step 3: Explore Federated Blocks under the Realm

![Screenshot 2025-07-11 at 07.50.50.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/6a39257801efe7b33cee5e3e909005c9/assets/Screenshot%202025-07-11%20at%2007.50.50.png)

👉 Step 4: View Delegated Block and Allocations - Click on AWS

![Screenshot 2025-07-11 at 07.45.41.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/3ea4af016011d4c307118ce040f67320/assets/Screenshot%202025-07-11%20at%2007.45.41.png)

👉 Step 5: Navigate to IP Spaces for Allocation View

![Screenshot 2025-07-11 at 07.45.51.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/8154ad96a8b19d94048888b1a8196e3e/assets/Screenshot%202025-07-11%20at%2007.45.51.png)


👉 Step 5: Navigate to IP Spaces for Allocation View

![Screenshot 2025-07-11 at 07.46.01.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/aafb462cf6851ce2e4a94933e86f4352/assets/Screenshot%202025-07-11%20at%2007.46.01.png)

👉 Step 6: Confirm Delegation and Federation in Detail

![Screenshot 2025-07-11 at 07.46.15.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/6a55d9afc56400f822ba1d608141b7d6/assets/Screenshot%202025-07-11%20at%2007.46.15.png)



# 🔐 2️⃣ Enforcement: No Overlapping Blocks
===

🧠 Simulate IP Conflict via Terraform: IPAM Enforcement in Action

In real-world scenarios, human error or misconfigured IaC can unintentionally attempt to reassign the same CIDR block to multiple resources. This is a common operational risk in large environments where multiple teams or automation pipelines interact.

➤ Simulation Step:
To demonstrate how Infoblox enforces IPAM policy and prevents overlapping allocations, attempt to provision the same CIDR block again.

Append the following Terraform block to your main.tf file under the ipam-test/ directory — specifically **at line 100** in the existing file:

![Screenshot 2025-07-11 at 11.26.51.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/92795209bb99e7d0da60351d35b26c55/assets/Screenshot%202025-07-11%20at%2011.26.51.png)


```
resource "bloxone_ipam_address_block" "duplicate_block" {
  address = "10.20.20.0"
  cidr    = 24
  name    = "duplicate-test"
  space   = bloxone_ipam_ip_space.ip_space_acme.id
  federated_realms = [data.bloxone_federation_federated_realms.acme.results[0].id]
}
```

🚀 Let’s Kick Off the Automation: Apply the Terraform Plan

Now that your configuration is ready, it’s time to bring it to life. This command will apply your infrastructure changes using Terraform, provisioning cloud resources based on the IPAM data coming from Infoblox UDDI.

```run
cd ~/infoblox-lab/uddi-ipam/terraform/ipam-test/
terraform apply --auto-approve
```

💡 This is where Infrastructure as Code (IaC) meets centralized IPAM control. Everything is deterministic, traceable, and aligned with your enterprise policies.

🛑 Expected Outcome:
When you run terraform apply, the Infoblox UDDI control plane will reject the request with an error like:

> [!IMPORTANT]
> **The ipam/address_block(10.20.20.0 - 10.20.20.255) already exists.**


![Screenshot 2025-07-11 at 11.25.12.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/b73dd0586a5a2d7537a8512d447b5907/assets/Screenshot%202025-07-11%20at%2011.25.12.png)

✅ This demonstrates how Infoblox UDDI enforces global IP uniqueness—catching misconfigurations at the source and preventing drift or collision across your infrastructure.



🧠 What This Shows:
- UDDI prevents overlapping IPs
- Enforcement is native and enforced at the API level
- Even Terraform can’t override this → infra-as-code meets IPAM policy


# 🛑 3️⃣ Simulate a Misuse via AWS Console
===


🔍 Bypass Test: Manually Create a Conflicting VPC in AWS Console

Head over to the AWS Console and try this:
	•	Manually create a new VPC using the same CIDR block: 10.0.20.0/24
	•	It will succeed — but here’s the catch:

🚫 It’s invisible to Infoblox UDDI
❌ There’s no tracking, tagging, or audit trail
⚠️ You’ve just created uncontrolled IP sprawl

🧠 Lesson: Without centralized IPAM like Infoblox, it’s easy for teams to unknowingly overlap and conflict — leading to painful troubleshooting and shadow infrastructure.


🖼️ Visual Walkthrough: Creating a Conflicting VPC via AWS Console

To better illustrate how manual VPC creation can bypass centralized IPAM, here’s a quick visual guide:

📸 Screenshots Below:

Follow the steps shown in these UI captures to manually create a conflicting VPC:

1. Navigate to the AWS Console in the left-hand panel of the Instruqt environment.

🧭 Use the Cloud credentials provided in Section 1) to log in securely.


2.	In the AWS Console, search for “VPC”, click on it, and ensure the region is set to EU-WEST-2 (London)

![Screenshot 2025-07-11 at 07.27.56.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/9e2a39a5e30f4bb75ba638223667d14c/assets/Screenshot%202025-07-11%20at%2007.27.56.png)

![Screenshot 2025-07-11 at 07.28.07.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/26ac29dd12955e9c217ea922120eb9b8/assets/Screenshot%202025-07-11%20at%2007.28.07.png)

3.	Click Create VPC

![Screenshot 2025-07-11 at 07.29.42.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/f91decae1aaf6957324752423c39e88d/assets/Screenshot%202025-07-11%20at%2007.29.42.png)

4. Choose the configuration options as shown in the screenshot below.

![Screenshot 2025-07-11 at 07.35.16.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/45e7307803935204f585c88b37e9bd21/assets/Screenshot%202025-07-11%20at%2007.35.16.png)

> [!IMPORTANT]
> Use 10.20.20.0/24 — this is the same range already allocated by Infoblox.

5.	Tag It If You Want (Optional)
But note — Infoblox won’t see this unless it’s managed via UDDI.

5.	Hit Create VPC at the bottom.

The VPC is created… but off the grid.
❌ No sync. No tagging. No central visibility.

📘 NOTE — New Infoblox IPAM UI Capability (Not Yet in This Lab Environment)
Infoblox recently introduced the UDDI IPAM Perspective, a major enhancement to the IP Address Management experience.

This feature is not yet enabled in the lab environment you’re using, but you will see it in production environments and future releases of this lab.
What the new feature adds:
- Automatically detects overlapping subnets across all discovered VPCs
- Visually highlights conflicting or duplicated ranges
- Displays complete address lineage (IP spaces → blocks → ranges → discovered ranges)
- Makes drift and misaligned allocations immediately obvious
- Provides a unified, cloud + on-prem source of truth for all IP activity


👉 Using UDDI + Terraform ensures safe, conflict-free IP allocations — eliminating overlaps entirely.


![Screenshot 2025-07-11 at 07.32.33.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/6c933df67f1576703e2a1820f00b2192/assets/Screenshot%202025-07-11%20at%2007.32.33.png)


Contrast that with your Terraform+UDDI flow:
- Traceability ✅
- Governance ✅
- No shadow IPs ✅


🏁 Summary: Why This Matters

|Capability |Manual AWS|Terraform + UDDI |
| -------- | -------- | -------- |
| IP Collision Protection | ❌| ✅|
| Centralized Visibility| ❌| ✅|
| Federation / Realm Enforcement| ❌| ✅|
| DNS Control Tie-in| ❌| ✅|
| Auditing & Change Tracking| ❌| ✅|


## Time for the Next Challenge

Click **NEXT**!


