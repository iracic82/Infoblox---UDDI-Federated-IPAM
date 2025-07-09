---
slug: review-architecture-and-deploy-resources
id: 4mavjdqwc4yr
type: challenge
title: Review Architecture and Deploy Resources
teaser: Review Architecture and Deploy Resources
notes:
- type: video
  url: https://cdn.instruqt.com/assets/instruqt/2024-036%20Instruqt%20101_Version%203.0.mp4
tabs:
- id: teyenwblx8lu
  title: Shell
  type: terminal
  hostname: shell
- id: f91heqdfmu8v
  title: Editor
  type: code
  hostname: shell
  path: /root/infoblox-lab
- id: u1nt6odtrug3
  title: AWS Console
  type: browser
  hostname: aws
- id: 0ojpvxstsr2e
  title: Azure Console
  type: browser
  hostname: azure
- id: huegpkvjgahs
  title: Infoblox Portal
  type: browser
  hostname: infoblox
- id: ktn24xalcvx4
  title: Lab Diagram
  type: browser
  hostname: lab
difficulty: ""
timelimit: 0
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---
In this lab, you will get hands-on with Infoblox Universal DNS Management, a single solution for
visibility and control of DNS tools used across on-premises, hybrid, and multi-cloud networks. You will
begin with a tour of the centralized visibility and management for DNS, exploring the efficiency of the
consolidated Infoblox Portal. Then, you’ll manage DNS records in Azure DNS and AWS Route 53, using
the same Universal DDI interface and workflow to make updates across clouds.


> [!IMPORTANT]
> **NOTE:** This environment is *real*! AWS and Azure Cloud Accounts have been created for each student. No bitcoin mining, please! :)

In this section we will:
1) Review the cloud architecture
2) Login to your cloud account console's
3) Deploy resources onto your cloud regions
4) Create your Infoblox Portal user

---

## 1) Review Cloud Architecture
===

First lets review the cloud architecture that has been provision for your Infoblox Lab experience.

Navigate to the *Lab Diagram* tab above and review the diagram. This is what we're building today!




## 2) Login to your cloud account consoles
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



## 3) Deploy resources onto your cloud regions
===

Now that you've logged into the cloud providers consoles its time to deploy resources for upcoming Instruqt Challenges:

### 1. Deploy AWS resources in EU

⚙️ Pre-deployed Infrastructure(AWS)

To save time and avoid long waits during the lab, core resources have already been provisioned in the background using Terraform. You don’t need to deploy everything from scratch.

You can verify this pre-deployment in two ways:

•	🔍 AWS Console – Navigate to the relevant services (EC2, VPC, TGW, etc.) and confirm that the resources are already in place according to the LAB Diagram.

•	🧾 Terraform Output – Run terraform output in the repo directory to view key variables and resource info like instance IPs, VPC IDs, etc.

```run
cd ~/infoblox-lab/Infoblox-PoC/terraform
terraform output
```

If you’re curious, the actual Terraform code used is available in the **Editor** window of this lab. Feel free to explore it and see how each resource is defined and managed.

Set up the DNS infrastructure with the appropriate VPC associations and A-records as outlined in the lab diagram.

```run
cd ~/infoblox-lab/Infoblox-PoC/terraform
terraform apply --auto-approve -target=aws_route53_zone.private_zone -target=aws_route53_record.dns_records
```

### 2. Deploy Azure resources in North Europe

⚙️ Pre-deployed Infrastructure (Azure)

To speed up the lab and avoid unnecessary provisioning time, the core Azure resources have already been deployed in advance using Terraform.

You can validate this pre-provisioned state in two simple ways:

•	🔍 Azure Portal – Head to the Resource Group where this lab is deployed and inspect VMs, VNets, subnets, etc. according to the LAB Diagram.

•	🧾 Terraform Output – Run terraform output in the working directory to get useful details like IP addresses, VNet names, and other variables used in the lab.

```run
cd ~/infoblox-lab/Infoblox-PoC/terraform
terraform output
```

Want to see how it all works? The Terraform code is fully visible in the **Editor** window, so feel free to poke around and understand the architecture.

Set up the DNS infrastructure with the appropriate Vnet associations and A-records as outlined in the lab diagram.


```run
cd ~/infoblox-lab/Infoblox-PoC/terraform
terraform apply --auto-approve -target=azurerm_private_dns_zone.private_dns_azone -target=azurerm_private_dns_zone_virtual_network_link.eu_vnet_links -target=azurerm_private_dns_a_record.eu_dns_records
```


## 4) Create Admin User to your Infoblox Portal Dashboard
===

> [!NOTE]
> Note: Use your Business Email for User Creation

Your user account and sandbox have already been created. The next step is to set up your password and activate your account.

> [!IMPORTANT]
> NOTE: If your account has already been activated on the Infoblox Portal, please proceed to the password reset steps outlined in Section 2.

### Section 1

1. Please check the inbox of the email account you used to register for the Infoblox Lab.
2. You will receive an email with the subject “Infoblox User Account Activation.” Open this email and click on the “Activate Account” button to proceed.

![Screenshot 2025-04-01 at 11.15.44.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/93d7e021e28c20d105ca34aace35d149/assets/Screenshot%202025-04-01%20at%2011.15.44.png)

4. A new browser window or tab will open, prompting you to create a new password. Please enter your desired password to complete the setup.

![Screenshot 2025-04-01 at 11.19.01.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/0fd5315d47a283fce641de81b289ac64/assets/Screenshot%202025-04-01%20at%2011.19.01.png)

5. Once you’ve set your password, close the newly opened tab or window. We’ll be logging in through the Instruqt tab labeled "Infoblox Portal".
6. In the Instruqt tab labeled "Infoblox Portal", log in using the credentials you set up in the previous steps.
7. After logging in, please mark the first window as shown in the example below. This confirms that you have successfully accessed the Infoblox Portal.

![Screenshot 2025-04-01 at 11.01.03.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/a082b5c7276e1c2e27eaaf7bee832089/assets/Screenshot%202025-04-01%20at%2011.01.03.png)

7. In the upper-left corner of the Infoblox Portal, click on the drop-down menu. Use the “Find Account” field to search for your sandbox by entering the "Sandbox-ID" shown below. It is important that you select your specific Sandbox-ID from the list and click on it to proceed.

**Your Sandbox ID**
```
[[ Instruqt-Var key="Sandbox_ID" hostname="shell" ]]
```

---


![Screenshot 2025-04-01 at 11.03.20.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/bdbf322902db478154c3fece79237f86/assets/Screenshot%202025-04-01%20at%2011.03.20.png)

---

### Section 2

🔐 Accessing the Infoblox Portal

If you’ve previously used your email to access the Infoblox SaaS platform, you do not need to create a new account.

✅ Existing User

1.	Go to Infoblox Portal TAB on the left.
2.	Login using your existing email address and password.
3.	Once authenticated, the lab tenant will be automatically added to your list of available tenants (you’ll see it in the top-right tenant switcher).

![Screenshot 2025-07-03 at 11.19.07.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/93f17f66e50b5a58f68e3e3d3953396a/assets/Screenshot%202025-07-03%20at%2011.19.07.png)

In order to RESET the password ( ONLY if required ) follow the steps below:


1. Please navigate to the Infoblox Portal page by clicking on the Infoblox Portal tab within the Instruqt lab environment. This will direct you to the appropriate login interface.
2. Once you’re on the Infoblox Portal page, click on “Need Assistance” located at the bottom of the login form.

![Screenshot 2025-04-01 at 10.52.47.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/0bacd7dc4193c2770df54b65c7eceb3a/assets/Screenshot%202025-04-01%20at%2010.52.47.png)

3. After clicking on “Need Assistance”, select “Forgot Password” from the available options to initiate the password reset process.

![Screenshot 2025-04-01 at 10.52.57.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/3971464a872c428ee8879f3d7287b201/assets/Screenshot%202025-04-01%20at%2010.52.57.png)

4. You will receive an email with the subject “Account Password Reset.” Open this email and click on the “Reset Password” button to proceed with setting a new password.

![Screenshot 2025-04-01 at 11.42.21.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/263657baa43cefce4e8fc2062d2371f1/assets/Screenshot%202025-04-01%20at%2011.42.21.png)

5. Once you’ve set up your password, please return to "Section 1" of the instructions and continue from Step 4 onward.




## Time for the Next Challenge

Now we've inspected the playing field its game time. Click **Check**!
