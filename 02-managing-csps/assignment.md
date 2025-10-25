---
slug: managing-csps
id: qutor4bzlfy6
type: challenge
title: Gain Visibility into Cloud  Environments
teaser: Managing Public Cloud Providers DNS  & IPAM
notes:
- type: video
  url: https://www.youtube.com/embed/7Ohhwuouw3A?si=m-BXbZGfPMEYS0z5
- type: video
  url: https://www.youtube.com/embed/H0t7P8mnXw4?si=IRqb9o-d-sHuXCnj
tabs:
- id: whwihuavueef
  title: Shell
  type: terminal
  hostname: shell
- id: j9m3kk6gfylh
  title: Editor
  type: code
  hostname: shell
  path: /root/infoblox-lab
- id: vnizldwv8lgu
  title: AWS Discovery
  type: browser
  hostname: aws-discovery
- id: 0atusfdhxeib
  title: AWS Console
  type: browser
  hostname: aws
- id: 9hgxhyxfuwb6
  title: Azure Console
  type: browser
  hostname: azure
- id: dnhhcddb02qu
  title: GCP Console
  type: browser
  hostname: gcp
- id: un6y2hyhhuym
  title: Infoblox Portal
  type: browser
  hostname: infoblox
- id: tgtfh3uwzy0t
  title: Lab Diagram
  type: browser
  hostname: lab
difficulty: ""
timelimit: 0
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---
🌐 Universal DDI Management™: The Backbone of Modern Network Services

Universal DDI Management™ is the industry’s first and most comprehensive SaaS-based solution for managing critical DNS, DHCP, and IPAM services across hybrid and multicloud environments. Think of it as your cloud-native command center for everything DDI.


![Screenshot 2025-07-03 at 20.31.01.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/6306bc2ffdcc552e684400d908c5a1fc/assets/Screenshot%202025-07-03%20at%2020.31.01.png)

🔧 What It Does

•	Central Hub

Provides a single SaaS control plane to configure and manage all your network services—whether they’re on-prem, in AWS, Azure, GCP, or anywhere else.

•	Comprehensive Consolidation

Unifies DNS, DHCP, and IP address management across:

•	Microsoft DNS - coming soon

•	BIND - coming soon

•	Infoblox NIOS and NIOS-X

•	Amazon Route 53

•	Azure DNS

•	Google Cloud DNS

•	Streamlined Operation

Speeds up service delivery by eliminating silos and unifying policy and configuration across the infrastructure.


⸻

![Screenshot 2025-07-03 at 20.35.07.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/1877f3b559d4ddb81b85a4109edf2208/assets/Screenshot%202025-07-03%20at%2020.35.07.png)

💡 Four Core Value Points

1.	🧭 Centralized Control

A single interface to configure, monitor, and manage DNS/DHCP/IPAM across any environment.

2.	🔌 Deep Integration

Bridges traditional DNS (like Microsoft and BIND) with modern cloud-native DNS platforms.

3.	⚙️ Operational Efficiency

Reduces management overhead, accelerates change delivery, and improves troubleshooting and governance.

4.	📈 Scalability and Flexibility

Whether you’re running bare metal, virtual appliances, or SaaS-native DNS like NIOS-X, it scales with your architecture.

# Infoblox UDDI Portal as a Single Pane of Glass

![Screenshot 2025-07-03 at 20.36.56.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/4cc380d19d95179f9e4ecae3023de36f/assets/Screenshot%202025-07-03%20at%2020.36.56.png)



The Infoblox Portal can be configured to manage DNS and IPAM data from public cloud providers like AWS, Azure, and GCP.

Complete the following steps to sync DNS  data from AWS and Azure.

## 1) Login to your cloud account consoles
===

🔐 (Optional) Log in to Your Cloud Account Consoles

You should already be signed in to the AWS,GCP and Azure web consoles via the embedded tabs on the left-hand side of the Instruqt interface.

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

## ☁️ Cloud Discovery Overview (AWS & Azure)
===

**Infoblox Universal Asset Insights** automatically discovers and tracks cloud resources using native cloud APIs.

This reduces manual overhead, keeps your inventory fresh, and enables deeper asset visibility across your multicloud environment.

⸻

🔹 AWS Discovery


Infoblox connects to AWS via a cross-account IAM role, which the platform assumes using a secure External ID. The following resources are discovered:

•	EC2 instances, VPCs, subnets

•	Route tables, NAT and Internet Gateways

•	Load Balancers (ALB, NLB)

•	Route 53 Hosted Zones and Records (with optional write access)

•	Tags, regions, and metadata


As part of the cloud discovery integration, Infoblox uses an IAM role named infoblox_discovery to securely access your AWS environment. This role defines the permissions Infoblox uses during synchronization jobs, such as reading resource metadata or managing DNS records (if enabled).

The role is assumed using a secure ExternalId, which ensures that only Infoblox can use it — even if the role ARN is exposed. This is a best practice for cross-account access with third-party integrations.

The screenshot below illustrates what a properly configured IAM role  looks like in the AWS Console (for the LAB environment):

![Screenshot 2025-07-09 at 08.54.34.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/8a5fbac55d713ee3a18864f2268d4a06/assets/Screenshot%202025-07-09%20at%2008.54.34.png)

![Screenshot 2025-07-09 at 08.54.22.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/4a968e8f80e1916de4c96b89e547296d/assets/Screenshot%202025-07-09%20at%2008.54.22.png)

⸻

🔹 Azure Discovery

Infoblox connects to Azure using a service principal (App registration) with a custom or built-in role assignment at the subscription or resource group level. Discovered resources include:

•	Virtual Machines and associated NICs

•	Virtual Networks (VNets), subnets, peerings

•	Network Security Groups, DNS zones and records

•	Resource groups, tags, and regional metadata

⸻

🔐 Azure Permissions Required for Universal DDI



✅ Minimum Roles Required


•	Reader:

Grants read-only visibility into Azure resources.

Used for IPAM sync, asset discovery, and general inventory collection.

✅ Safe default for read-only discovery.

NOTE: For more information, see [Reader role](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles/general#reader).

⸻

•	DNS Zone Contributor:


Full management of public DNS zones and record sets.

❌ Does not grant access control (RBAC).

NOTE: For more information, see [DNS Contributor role](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#dns-zone-contributor)

⸻

•	Private DNS Zone Contributor:

Same as above, but scoped to private DNS zones.

❌ Does not control virtual network links.

NOTE: For more information, see [Private DNS Zone Contributor](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#private-dns-zone-contributor).

⸻


⚙️ Resource Group Management


If your setup creates or manages resource groups, the following actions are required:


•	Microsoft.Resources/subscriptions/resourceGroups/write

•	Microsoft.Resources/subscriptions/resourceGroups/delete



📌 Used when the deployment dynamically creates resource groups for forwarders or discovery.


⸻

🧾 App Registration Prerequisites


To register an application (service principal), your Azure user must have the:


•	Cloud Application Administrator role

•	Fulfill [App Registration prerequisites](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app#prerequisites)



⸻


🔍 Permissions Required for Cloud Forwarder Discovery Only


If you only need to read DNS Resolver config, the following permissions are sufficient:


```
•	Microsoft.Network/dnsResolvers/read

•	Microsoft.Network/dnsResolvers/inboundEndpoints/read

•	Microsoft.Network/dnsResolvers/outboundEndpoints/read

•	Microsoft.Network/dnsForwardingRulesets/read

•	Microsoft.Network/dnsForwardingRulesets/forwardingRules/read

•	Microsoft.Network/dnsForwardingRulesets/virtualNetworkLinks/read
```

⸻
## 2) 🔍 Onboarding AWS, Azure and GCP Accounts to Infoblox Portal (Pre-Provisioned)
===


The AWS Cloud Discovery job has been pre-provisioned for you — no need to run the CloudFormation stack or fetch Principal/External IDs.

What You Need to Do

1. Open the Infoblox Portal

Go to:
Configure → Networking → Discovery

2. Click the Cloud tab

You’ll see the pre-created AWS Discovery job listed there.

3. Click Edit on the existing job

Open the job to review the configuration.

## 3) 🔍 Review Existing On-Prem IPAM with Federated Realms
===

Before diving into IaC automation or cloud asset visibility, let’s first explore how IP space is structured and governed within Infoblox UDDI. This challenge focuses on understanding how federated realms and delegated blocks form the foundation of centralized IP management.

👉 Note: Federation, delegation, and policy enforcement will be covered in more depth in the next challenge—along with the Terraform automation workflow.


✅ Steps:
1.	Log into the Infoblox UDDI Web Console.
2.	From the left-hand menu, go to Configure → Networking → IPAM Realms.
3.	Select the ACME Corporation Federated Realm.
4.	Inspect how top-level blocks are structured (AWS, Azure, GCP,On-prem).


📌 Goal: Understand how IP address planning and hierarchy is governed before automation kicks in.


### 🔍 Screenshot Walkthrough


👉 Step 1: Navigate to IPAM Realms

![Screenshot 2025-07-11 at 07.45.01.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/380dd567f7bad3e7309e2c62c25967cd/assets/Screenshot%202025-07-11%20at%2007.45.01.png)

👉 Step 2: Locate the Federated Realm (ACME Corporation)

![Screenshot 2025-07-11 at 07.45.09.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/060b79dbd1b9e95b3d4b2c88efd2b9c4/assets/Screenshot%202025-07-11%20at%2007.45.09.png)


👉 Step 3: Explore Federated Blocks under the Realm

![Screenshot 2025-07-11 at 07.50.50.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/6a39257801efe7b33cee5e3e909005c9/assets/Screenshot%202025-07-11%20at%2007.50.50.png)




## 4) 🔍 UDDI Explore and Visibility of Assets
===


In this section, we validate the end-to-end visibility of assets and DNS data across cloud environments using Infoblox UDDI.

Open and login to Infoblox UDDI Portal.

✅ Step 1: Verify Discovery Sync

We navigate to Configure > Networking > Discovery to confirm that discovery jobs for AWS, Azure and GCP jobs.


![Screenshot 2025-08-20 at 11.06.18.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/00d2edc95e6b6d25047b74b9f3732a08/assets/Screenshot%202025-08-20%20at%2011.06.18.png)


🌐 Step 2: Explore AWS DNS Zones

Please login to the Infoblox Portal:

**Under Configure →Networking →DNS → Zones**,  review the AWS-hosted zone created earlier — inspect its records inside the Infoblox **default** DNS View, where all zones are consolidated:

![Screenshot 2025-07-03 at 06.14.04.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/9b1e2fbe2c9081f55274cc2225e4ea5b/assets/Screenshot%202025-07-03%20at%2006.14.04.png)

We validate the zone infolab.com has been successfully pulled from Route 53.
Confirmed record sync with A records like:



app1.infolab.com → 10.20.0.100

app2.infolab.com → 10.20.2.100

app3.infolab.com → 10.20.3.100


![Screenshot 2025-07-03 at 06.14.22.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/76c2aaa37ddb76fcac7243a0bb4ebadc/assets/Screenshot%202025-07-03%20at%2006.14.22.png)


We then add a new record under →** Create/Record/A Record**:

app4.infolab.com → 10.10.10.9

![Screenshot 2025-07-03 at 06.14.46.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/efc477a969e766921118f016ef4ef50f/assets/Screenshot%202025-07-03%20at%2006.14.46.png)

Please add the record following the information from the screenshot below:

![Screenshot 2025-07-03 at 06.15.46.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/0d43827414734f7784192f169e21867d/assets/Screenshot%202025-07-03%20at%2006.15.46.png)

After saving, we switch to AWS Web Console  - login using provided credentials.

In the search field we type Route53 and click on it.

> [!IMPORTANT]
> NOTE: Make sure you are un EU-WEST-2 AWS Region in London.

![Screenshot 2025-07-03 at 06.48.01.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/8bd9f0ac00c19e46b70ee191d519f9c3/assets/Screenshot%202025-07-03%20at%2006.48.01.png)

Please on the lefthand side select Hosted Zones and you will see infolab.com - Click on it and verify the new A record is reflected, confirming successful sync back to Route 53.

![Screenshot 2025-07-03 at 06.48.48.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/1ea601172c767b90bbfeb68b05286c91/assets/Screenshot%202025-07-03%20at%2006.48.48.png)

![Screenshot 2025-07-03 at 06.18.01.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/6ec36f8d72799bd4184b4b8aca31b465/assets/Screenshot%202025-07-03%20at%2006.18.01.png)


🏢 Step 3: Explore Azure DNS Zones

We switch to the Azure DNS view in Infoblox Portal  following: ** Configure →Networking →DNS → Zones**



Confirmed zone infolab.com exists and DNS records such as:

azure-webprodeu1.infolab.com → 10.10.1.100

azure-webprodeu2.infolab.com → 10.10.2.100

Confirm that these were pulled from Azure Private DNS that has been created.


![Screenshot 2025-10-25 at 22.16.34.png](https://play.instruqt.com/assets/tracks/l95dr3nibefy/77ae3c1832e8eb487ec9294d0f258bf7/assets/Screenshot%202025-10-25%20at%2022.16.34.png)


📊 Step 4: Inspect IPAM Data

In Infoblox Portal please Navigate to **Configure →Networking →IPAM/DHCP**  to ensure that cloud assests like VPCs, subnets, route tables etc from both AWS and Azure are discovered.

![Screenshot 2025-07-03 at 07.01.10.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/3cd9dc60dd0533eb9b1ca18e7e9bcdb9/assets/Screenshot%202025-07-03%20at%2007.01.10.png)

Validate the view - you have option to toggle FLAT option view as well on the right

![Screenshot 2025-07-03 at 07.10.35.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/efd531faa99b32aea675b6cff15661d0/assets/Screenshot%202025-07-03%20at%2007.10.35.png)

![Screenshot 2025-07-03 at 07.11.50.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/ed8f1957e6c42ff90b8e2333d8deef08/assets/Screenshot%202025-07-03%20at%2007.11.50.png)

🖱️ You can click on any discovered item (such as IPs, subnets etc ) to drill down for more details like Attributes and Metadata of the assets:

Example shown in the screenshot below.

![Screenshot 2025-07-03 at 07.14.57.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/208fad4d2737bcbf6352bb783f5d98a8/assets/Screenshot%202025-07-03%20at%2007.14.57.png)


📈 Asset Visibility with UDDI – Unified View

With UDDI now actively syncing asset metadata across AWS and Azure, we can inspect what Infoblox surfaces as enriched visibility.

🔍 Step 1: Launch the Monitor Dashboard

In the Infoblox Cloud Console, on the left-hand menu:
Click Monitor

![Screenshot 2025-07-03 at 07.20.46.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/e96d6a86a9f737683ff97c8d1fc1d7f7/assets/Screenshot%202025-07-03%20at%2007.20.46.png)

At the bottom of the screen, select the Assets tab.

![Screenshot 2025-07-03 at 07.17.10.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/66953a1dd203b17c8bd74a9ff56fa05b/assets/Screenshot%202025-07-03%20at%2007.17.10.png)


This will present you with a visual dashboard of all discovered cloud assets.

🖱️ You can click on any chart or widget to drill down into more granular detail — for example:

	Asset classification (Zombie, Orphan, Ghost)
	Noncompliant assets (e.g., publicly exposed or unencrypted)
	DNS visibility (missing PTR/FWD records)
	IPAM coverage
	Asset location breakdown (CrowdStrike tags, regions)


	📊 What You’ll See
	•	Asset by Type – Server, Workstation, DNS, etc.
	•	Zombie/Orphan/Ghost breakdown
	•	Assets with Missing Records – great to see DNS hygiene issues
	•	Noncompliant Assets – Exposed or weak posture
	•	New Assets by Type – shows what was recently discovered
	•	Asset Locations – mapped by source tagging or EDR/CMDB sources


🧠 Pro Tip:
Click on any individual slice  — it’ll open up a filtered view of the exact assets impacted, letting you see more advanced details and troubleshoot DNS visibility, identify risky resources, or correlate cloud-native tags.

![Screenshot 2025-07-03 at 07.24.00.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/1de3f81355f92bb6e43d66f252c996a6/assets/Screenshot%202025-07-03%20at%2007.24.00.png)

## Time for the Next Challenge

Click **NEXT**!






