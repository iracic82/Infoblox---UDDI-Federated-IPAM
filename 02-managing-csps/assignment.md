---
slug: managing-csps
id: qutor4bzlfy6
type: challenge
title: Managing Public Cloud Providers
teaser: Managing Public Cloud Providers DNS  & IPAM
notes:
- type: video
  url: https://www.youtube.com/embed/7Ohhwuouw3A?si=m-BXbZGfPMEYS0z5
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
- id: un6y2hyhhuym
  title: Infoblox Portal
  type: browser
  hostname: infoblox
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
Using the credentials below, login to the AWS and Azure Web Consoles in their respective tabs above:

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

**AZURE USERNAME**
```
[[ Instruqt-Var key="INSTRUQT_AZURE_SUBSCRIPTION_INFOBLOX_TENANT_USERNAME" hostname="shell" ]]
```

**AZURE PASSWORD**
```
[[ Instruqt-Var key="INSTRUQT_AZURE_SUBSCRIPTION_INFOBLOX_TENANT_PASSWORD" hostname="shell" ]]
```

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

## 2) Onboarding AWS account onto Infoblox Portal
===

Before integrating AWS Route 53 with Universal DDI, you must first define the type of AWS Route 53 deployment you are using. Defining the type of AWS Route 53 deployment is required since each type of deployment has different configuration parameters that will be used while configuring network discovery in Universal DDI.

We are going to use -> Account Preference: Auto-Discover Multiple (Recommended)/Type of Access: Principal ID + Role ARN

### Step-by-Step Guide: AWS Discovery Configuration via Infoblox Portal

#### 1. Retrieve Required Identifiers

To proceed with the AWS Discovery configuration, you will need the following information:
	•	Principal ID
	•	External ID

Ensure you have this information available before continuing.

#### 2. Access the Infoblox Portal
Navigate to the Infoblox Portal.
From the top navigation menu, go to:
Configure → Networking → Discovery.

![Screenshot 2025-04-01 at 14.48.39.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/cfc6dc6a631168ae06d7c764a9a801e4/assets/Screenshot%202025-04-01%20at%2014.48.39.png)


#### 3. Configure AWS Discovery
1.	Within the Discovery section, select the Cloud tab.
2.	Click on Create AWS to begin setting up cloud discovery for AWS.

![Screenshot 2025-04-01 at 14.48.52.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/fe1b7255159d83b15197cb94b32acb62/assets/Screenshot%202025-04-01%20at%2014.48.52.png)

![Screenshot 2025-04-01 at 14.49.02.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/a9c0812f8d60b1139b442d5408128128/assets/Screenshot%202025-04-01%20at%2014.49.02.png)

NOTE: Gather information from the portal about External ID and Principal ID.

#### 4. Go to the AWS Discovery Page in Instruqt and click on Deploy to AWS.

#### 5. Log in to the console using the CSP credentials provided in "Section 1".

#### 6. Provide a name for the CloudFormation stack and enter the External ID captured in the previous steps.


> 	 > [!NOTE]
> Note: Leave the Account ID unchanged and COPY/PASTE External ID from the Infoblox Portal.


![Screenshot 2025-04-02 at 07.31.45.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/006976dbb7fd80357a9de266b7fac38f/assets/Screenshot%202025-04-02%20at%2007.31.45.png)


#### 7.Click "Next" on each page, keeping all settings at their default values.

![Screenshot 2025-04-02 at 07.32.00.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/71731c4542146913684191904516f770/assets/Screenshot%202025-04-02%20at%2007.32.00.png)

#### 8.Click "Submit" on the next page

![Screenshot 2025-04-02 at 07.32.13.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/2e75569517648689ca0b3066dcb3ae3a/assets/Screenshot%202025-04-02%20at%2007.32.13.png)


#### 9.Wait for the CloudFormation stack creation to complete, then navigate to the "Outputs" tab to retrieve the ARN value.

![Screenshot 2025-04-02 at 07.32.32.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/7fee78206bf25f20375773080bc131ab/assets/Screenshot%202025-04-02%20at%2007.32.32.png)

![Screenshot 2025-04-02 at 07.32.54.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/8db17c8d0ef84878d624e455488f66eb/assets/Screenshot%202025-04-02%20at%2007.32.54.png)

![Screenshot 2025-04-02 at 07.33.43.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/865b2d54d8605e47fcd41dfe771206b0/assets/Screenshot%202025-04-02%20at%2007.33.43.png)


#### 10.Return to the Infoblox Portal where you initiated the AWS Discovery Job, paste the retrieved ARN value into the appropriate field, and click "Next" to proceed.

![Screenshot 2025-04-02 at 07.34.15.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/343c6524235311f03e50805911807fdf/assets/Screenshot%202025-04-02%20at%2007.34.15.png)

#### 11.On the next page, configure the settings to match those shown in the screenshot below, then click "Next" to continue.

![Screenshot 2025-04-02 at 07.34.23.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/f331a4ac1d859b913b6096a122e829eb/assets/Screenshot%202025-04-02%20at%2007.34.23.png)

#### 12.On the next page, configure the settings to match those shown in the screenshot below, then click "Next" to continue.

![Screenshot 2025-07-08 at 11.04.49.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/589c137fa4fafd5ac6e5b919835aef74/assets/Screenshot%202025-07-08%20at%2011.04.49.png)

#### 13.On the next page, configure the settings to match those shown in the screenshot below, then click "Save&Close" to continue.

![Screenshot 2025-04-02 at 07.35.12.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/2e4b1289d89ffef13e65fe28f151410d/assets/Screenshot%202025-04-02%20at%2007.35.12.png)



## 3) Onboarding Azure account onto Infoblox Portal
===

Azure DNS is a cloud DNS web service that routes end users’ requests to internet applications and resources by resolving domain names into IP addresses and IP addresses into domain names. In Azure, DNS records are organized into hosted zones, which are configured through the Azure API, Azure CLI, or Azure Resource Manager.

Universal DDI provides the capability for synchronizing and integrating public-hosted zones with Azure, and this allows users to view and manage Azure DNS data through the Infoblox Portal. Also, BloxOne NIOS-X Servers can be configured to service zones synchronized from Azure.


The Infoblox Azure DNS integration feature offers the following:

Two-way synchronization of public-hosted zones and records between Azure and Universal DDI after the initial configuration and sync is complete. Synchronization of Azure DNS resource records configured with a simple routing policy is supported. Other routing policies are not supported. Synchronization of DNSSEC records is not supported.

One-way synchronization of private zones from Azure DNS to Universal DDI. The synchronized zones are read-only.

Viewing and management of Azure-NIOS-X hosted zones and records through the Infoblox Portal.

A NIOS-X Server can directly respond to DNS queries from clients for private zones that are managed in Azure. A NIOS-X Server can be configured as a secondary DNS server for local clients thereby reducing the network load since the queries do not need to recurse to Azure DNS.

### Step-by-Step Guide: AWS Discovery Configuration via Infoblox Portal

#### 1. Navigate to the Infoblox Portal and go to Configure → Administration → Credentials.

![Screenshot 2025-04-02 at 21.47.14.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/f1ba860ea63974329f57911a5bbcad83/assets/Screenshot%202025-04-02%20at%2021.47.14.png)

#### 2. Click Create and select Microsoft Azure from the dropdown menu.

![Screenshot 2025-04-02 at 21.47.48.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/1b8e062242f5ed8318d4aceaa3e9847b/assets/Screenshot%202025-04-02%20at%2021.47.48.png)



#### 3. Fill in all required fields marked with an asterisk (*) using the details provided below and click "Save&Close".

> [!IMPORTANT]
> NOTE: Please do not forget to give it a Name at the top.


**AZURE Tenant ID**
```
[[ Instruqt-Var key="INSTRUQT_AZURE_SUBSCRIPTION_INFOBLOX_TENANT_TENANT_ID" hostname="shell" ]]
```

**AZURE Client ID**
```
[[ Instruqt-Var key="INSTRUQT_AZURE_SUBSCRIPTION_INFOBLOX_TENANT_SPN_ID" hostname="shell" ]]
```

**AZURE Client Secret**
```
[[ Instruqt-Var key="INSTRUQT_AZURE_SUBSCRIPTION_INFOBLOX_TENANT_SPN_PASSWORD" hostname="shell" ]]
```


#### 4. Access the Infoblox Portal

1.	Navigate to the Infoblox Portal
2.	From the top navigation menu, go to:

Configure → Networking → Discovery.


#### 5. Configure Azure Discovery
1.	Within the Discovery section, select the Cloud tab.
2.	Click on Create Azure to begin setting up cloud discovery for Azure.


#### 6. Fill in all required fields marked with an asterisk (*) using the details provided below.

![Screenshot 2025-04-02 at 22.01.10.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/6cbc9dd38a1dc014d2ddb8ed7df4ac4f/assets/Screenshot%202025-04-02%20at%2022.01.10.png)

> [!IMPORTANT]
> Please give it a name and Select "Type of Access" -> Static ------->  under" Credentials" select the one you have created in the previous step.

Azure subscription id can be found below.

**AZURE SUBSCRIPTION ID**
```
[[ Instruqt-Var key="INSTRUQT_AZURE_SUBSCRIPTION_INFOBLOX_TENANT_SUBSCRIPTION_ID" hostname="shell" ]]
```

#### 7.On the next page, configure the settings to match those shown in the screenshot below, then click "Next" to continue.

![Screenshot 2025-04-02 at 22.09.04.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/098541c13a407a9df0da2581d6f2970b/assets/Screenshot%202025-04-02%20at%2022.09.04.png)

#### 8.On the next page, configure the settings to match those shown in the screenshot below, then click "Next" to continue.

![Screenshot 2025-04-02 at 22.10.42.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/6b6c728e758842db9ca7325b6a5cad7b/assets/Screenshot%202025-04-02%20at%2022.10.42.png)

#### 9.On the next page, configure the settings to match those shown in the screenshot below, then click "Save&Close" to continue.

![Screenshot 2025-04-02 at 22.11.18.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/51b0aaef0a1de4b8cdba1bf96735eb2a/assets/Screenshot%202025-04-02%20at%2022.11.18.png)

## 4) 🔍 UDDI Explore and Visibility of Assets
===


In this section, we validate the end-to-end visibility of assets and DNS data across cloud environments using Infoblox UDDI.

Open and login to Infoblox UDDI Portal.

✅ Step 1: Verify Discovery Sync

We navigate to Configure > Networking > Discovery to confirm that discovery jobs for both AWS and Azure are in a **Synced** state:

> [!IMPORTANT]
> NOTE: It will take around 2 x sync job interval ( 15mins each ) for the Discovery jobs to get synced.

![Screenshot 2025-07-03 at 06.13.17.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/806b671c5740f908a52bd6b756010b22/assets/Screenshot%202025-07-03%20at%2006.13.17.png)


🌐 Step 2: Explore AWS DNS Zones

Please login to the Infoblox Portal:

**Under Configure →Networking →DNS → Zones**, we explore the AWS-specific DNS view we have created in previous steps:

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

azure-webprodeu2.infolab.com → 10.30.1.100

Confirm that these were pulled from Azure Private DNS that has been created.

![Screenshot 2025-07-03 at 06.19.40.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/0d9b3b32c7862b9a7061d01e7a992edd/assets/Screenshot%202025-07-03%20at%2006.19.40.png)


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






