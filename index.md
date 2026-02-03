---
layout: default
title: Cloud Administration Basics I 
---

# 1. First Steps

## 1.1 Login to IBM Cloud Portal

The first step to working with IBM Cloud is logging into the IBM Cloud Portal.

1. Open the login page: [IBM Cloud Login](cloud.ibm.com/login)
2. Enter your credentials (username and password)
3. Confirm the login to gain access to the IBM Cloud Dashboard

<img src="{{ site.baseurl }}/screenshots/IBMCloud_Login.png" alt="IBM Cloud Login" width="550">

---

## 1.2 Enable Multi-Factor Authentication (MFA)

After logging into the IBM Cloud Account, the first step should be to enable Multi-Factor Authentication (MFA).

**Why MFA?**

A password-only protected account no longer meets current security requirements. MFA is already standard in many areas such as banking or social networks and is also **recommended as a best practice** in IBM Cloud.

**To enable MFA, follow these steps:**

1. Navigate to `Manage` in the top bar and select the `Access (IAM)` submenu
2. In the left sidebar, click on `Settings`
3. Under `Settings`, switch to `Authentication`

**Here you can now select how MFA should be set up. The recommended setting is:**

- **MFA for a user with an IBMid**
- **Either**, enable MFA for federated and non-federated users

<img src="{{ site.baseurl }}/screenshots/MFA1:2.png" alt="MFA" width="1500">

<img src="{{ site.baseurl }}/screenshots/MFA2:2.png" alt="MFA" width="1500">

---

## 1.3 Account Settings / Activating a Subscription

To find important information such as the account name or account ID, as well as to redeem subscriptions and manage other settings such as:

- Financial Services Validated
- EU Supported
- HIPAA Supported
- Enterprise-managed IAM
- Commercial Proof of Concept (PoC)
- Virtual Routing and Forwarding
- Service Endpoints

**Proceed as follows:**

1. Navigate to `Manage` in the top bar
2. Select the `Account` submenu
3. Click on `Account Settings` in the sidebar

<img src="{{ site.baseurl }}/screenshots/Settins1-2.png" alt="AccSettings" width="1500">

<img src="{{ site.baseurl }}/screenshots/Settings2-2_.png" alt="AccSettings" width="1500">

---

# 2. Working with Resource Groups

## 2.1 Resource Groups Explained

Resource groups are **logical containers** that organize related cloud resources (VMs, databases, etc.). They serve as central anchor points to **apply IAM access policies to the entire group**, simplifying permission management. They also enable **clear cost tracking (billing)** and **easy, isolated management** of the entire lifecycle of the contained resources.

<img src="{{ site.baseurl }}/screenshots/Ressourcengruppen.png" alt="Resource Groups Explained" width="1500">

The physical location of the resources is irrelevant for grouping. A resource group can contain resources that have been deployed across different geographic zones and regions.

<img src="{{ site.baseurl }}/screenshots/res_grp_zonen.png" alt="Resource Groups Zones" width="1500">

---

## 2.2 Creating Resource Groups

Plan your hierarchy before creating the first resource group. Consider whether organization by environments (Dev/Test), projects, or teams is best suited for your case. Consider how you want to assign permissions, allocate costs, and manage resources within the team.

**A resource group is created as follows:**

1. Navigate to `Manage` in the top bar
2. Select the `Account` submenu
3. Click on `Account resources` in the left sidebar
4. Navigate to the `Resource groups` submenu
5. On the right side, you can now click on `Create +`

<img src="{{ site.baseurl }}/screenshots/create_rc_grp_.png" alt="Create Resource Group" width="1500">

---

# 3. Identity and Access Management (IAM)

## 3.1 IAM Overview

### Identity Management (Manage Identities)

- **Trusted Profiles:** Enable secure, passwordless authentication for compute resources (e.g., clusters, VPCs) or federated users. They eliminate the need to manage long-lived credentials in applications.

- **Service IDs:** Identities for applications, tools, and automated processes. Since they are decoupled from human users, workflows remain stable even when employees change.

- **API Keys:** Credentials for authentication via CLI or API. They can be assigned to either a personal user account or a service ID to perform actions programmatically.

- **Identity Providers:** Enables connection of external corporate directories (e.g., via SAML or OpenID Connect). Users authenticate with their existing corporate credentials (Single Sign-On).

### Access Control (Manage Access)

- **Access Groups:** The most important tool for efficient permission management. IAM policies are assigned to the group once. All members (users, service IDs) automatically inherit these permissions.

- **Authorizations:** Control direct access between IBM Cloud Services (service-to-service), without involving a user identity (e.g., a Kubernetes cluster may access a Container Registry).

- **Roles:** Define the specifically allowed actions. IBM distinguishes between `Platform Roles` (management of COS, e.g., create/delete) and `Service Roles` (usage of COS, e.g., read/write data).

<img src="{{ site.baseurl }}/screenshots/IAM_overview.png" alt="IAM Overview" width="1500">

**Accessing IAM Management:**

1. Click on `Manage` in the top navigation bar
2. Select `Access (IAM)` from the dropdown menu

In the left sidebar, you will then find an overview of all available IAM options and settings.

<img src="{{ site.baseurl }}/screenshots/IAM_overview2.png" alt="IAM Overview 2" width="1500">

---

## 3.2 Access Policies and Access Groups

**Access Policy:**

An Access Policy is the actual ruleset that defines who (subject) can do what (resource) and how (role). It essentially consists of:

- The target resource (e.g., "All Kubernetes Clusters in Resource Group X")
- The role (e.g., Viewer or Administrator)

**Access Groups:**

An Access Group is a logical container that bundles different identities (users, service IDs, trusted profiles). It serves efficient management: Instead of assigning permissions to each user individually, you simply add the user to a group (e.g., Admins or Dev-Team). They then automatically inherit all rights of this group.

**Best Practice:**

In practice, you create an Access Policy and assign it to an Access Group, which you then assign to users.

Individual policies are difficult to maintain (not scalable). If you assign permissions directly to individual users, you must manually edit each user and remove each policy individually when changes occur (e.g., team changes or employee departure). This is extremely time-consuming and error-prone (security risk due to forgotten permissions).

---

## 3.3 Creating Access Groups (Platform Admin Group)

Creating a Platform Admin Access Group is one of the most important first steps in any new IBM Cloud Account.

**Why do we create it first?**

Initially, only the Account Owner has full administrative rights. This poses a massive risk (Single Point of Failure): If the Owner leaves the company or loses access, the entire account becomes inoperable.

For this reason, we create this group before any other configuration takes place to create redundancy.

**Purpose of the Group:**

This group contains the administrators who technically manage the account (invite users, view billing, control IAM), without having to use the Account Owner login.

**Recommended Permissions:**

This group typically receives the highest rights, such as:

- Administrator role on All Account Management Services (for Billing, Support, User Management)
- Administrator role on All Identity and Access enabled services (to grant rights to other teams)

**Follow these steps to create the group for administrators and equip it with the necessary rights:**

1. Navigate to `Manage` in the top bar of the IBM Cloud Console
2. Select `Access (IAM)` from the dropdown menu
3. Orient yourself in the left sidebar to the `Manage Access` section
4. Click on the `Access groups` submenu there
5. Start creating a new group by clicking the blue `Create +` button
6. Give the group a unique name (e.g., Platform-Admins) and a brief description. Then confirm with `Create`
7. You are now in the overview of the new group. Click on `Access` in the tab bar at the top
8. Click on the blue `Assign access +` button to start the permission assignment process
9. In the first step, select `All Account Management Services` under "Service" (this controls access to Billing, User-Invites, etc.)
10. Scroll to "Roles and actions" and check the `Administrator` role
11. Click the `Add` button at the bottom to note this rule
12. Now create the second policy directly: This time select `All Identity and Access enabled services` as the service (this enables access to all resource instances)
13. Under "Roles and actions", also select the `Administrator` role again
14. Add this second rule as well with a click on `Add`
15. On the right side, you will now see a summary of the noted policies in the Summary section. Review the selection and finalize the process with a click on `Assign`

<img src="{{ site.baseurl }}/screenshots/admin_agrp1.png" alt="Admin Access Group 1" width="1500">

<img src="{{ site.baseurl }}/screenshots/admin_agrp2.png" alt="Admin Access Group 2" width="1500">

<img src="{{ site.baseurl }}/screenshots/admin_agrp3.png" alt="Admin Access Group 3" width="1500">

<img src="{{ site.baseurl }}/screenshots/admin_agrp4_.png" alt="Admin Access Group 4" width="1500">

---

## 3.4 Inviting Users (Admins)

To grant new employees or users access to your IBM Cloud account, they must be explicitly invited.

**Follow these steps:**

1. Navigate to `Manage` in the top bar
2. Click on `Access (IAM)`
3. Select `Manage identities` in the left sidebar
4. Select the `Users` option
5. Now click on the blue `Invite users +` button
6. Choose between `Access groups` and `Access policy`
7. Select your Platform Admin `Access group`
8. Finally, click on `Invite` to invite the users

<img src="{{ site.baseurl }}/screenshots/invite_useres1.png" alt="Invite Users 1" width="1500">

<img src="{{ site.baseurl }}/screenshots/invite_users2.png" alt="Invite Users 2" width="1500">

---

## 3.5 Concept: Platform Access vs. Service Access

A common misunderstanding in IAM is the difference between managing the resource itself and using the data contained within it. IBM Cloud strictly separates these permissions.

This can best be explained using the example of Cloud Object Storage (COS):

### 1. Platform Access (Managing the "Shell")

Platform Access refers to actions that take place at the IBM Cloud Console level. It's about controlling the lifecycle of the service, not its content.

**Focus:** Management of the service instance

**Typical Roles:** Viewer, Editor, Administrator

**COS Example:**

- A user with the Editor role can create a new COS service instance or change the instance name
- They can assign the instance to a resource group
- **But:** They cannot (without Service Access) see which files are in the buckets or upload files

### 2. Service Access (Using the "Content")

Service Access refers to actions that take place within the service, mostly via API calls or direct data operations. It's about access to the actual data.

**Focus:** Using the API and data manipulation

**Typical Roles:** Reader, Writer, Manager

**COS Example:**

- A user with the Writer role can upload or delete files (objects) to a bucket
- A user with the Reader role can download files
- **But:** They cannot delete the COS instance itself or invite other users to it

<img src="{{ site.baseurl }}/screenshots/platform:service.png" alt="Platform vs Service Access" width="1500">

<img src="{{ site.baseurl }}/screenshots/platform:service_excalidraw_.png" alt="Platform vs Service Access Diagram" width="1100">

---

## 3.6 Creating Custom Roles

When standard roles (such as Viewer, Editor, Admin) are too imprecise or grant too many rights, Custom Roles come into play. They enable tailored access control according to the Least-Privilege principle (users receive only the minimally necessary rights).

**How it works:**

Instead of adopting a ready-made role package, you select specific service actions from a list and bundle them into a new role.

**Example:**

You want an operator to be able to restart and stop virtual servers, but they should not have permission to delete servers or create new ones.

- **Standard Editor role:** Would be too powerful (can also delete)
- **Custom Role:** You create a role called "VM-Operator" and add only the actions instance.start and instance.stop

**To create a custom role, navigate as follows:**

1. Go to `Manage` in the top bar
2. Select `Access (IAM)`
3. Click on `Roles` in the left sidebar
4. Start the process with a click on `Create +`

In the subsequent menu, define the role's properties. First, assign a meaningful name and description. Then select the target service and add the desired permissions (Actions) granularly. Once you have selected all actions, finalize the creation via the Create button.

<img src="{{ site.baseurl }}/screenshots/custom_roles_1.png" alt="Custom Roles 1" width="1500">

<img src="{{ site.baseurl }}/screenshots/custom_roles_2.png" alt="Custom Roles 2" width="1500">

---

## 3.7 Context Based Restrictions (CBR)

Context Based Restrictions (CBR) extend classic IAM with another crucial dimension.

While IAM exclusively controls **who (identity)** may access a resource, CBR additionally defines **from where (network context)** this access must occur. It thus functions as a network-based security layer that is checked after successful authentication.

**The concept is based on two main components:**

### 1. Rules

Here you link a zone with a Cloud Service. A rule states, for example: "Access to Cloud Object Storage Bucket X is only allowed if the request comes from the 'Company-VPN' zone."

**Why is this important?**

Through this additional dimension, CBR effectively protects against Credential Theft. Even if an attacker steals a valid API key (the "Who" is correct), access is denied because they are not coming from the secure corporate network (the "Where" is wrong).

### 2. Network Zones

Here you define trusted origins. A zone is an "allowlist" and can include:

- Specific IP address ranges (e.g., the company VPN)
- Other IBM Cloud VPCs
- Service References (to authorize Cloud Services among themselves)

**To set up Context-Based Restrictions, navigate as follows:**

1. Go to `Manage` in the top bar
2. Select `Context-based restrictions`
3. Then select the desired area: `Rules` or `Network zones`

<img src="{{ site.baseurl }}/screenshots/cbr1.png" alt="CBR Setup" width="1500">

### Network-Based vs. Identity-Based Protection

When does CBR make sense?

<img src="{{ site.baseurl }}/screenshots/cbr2.png" alt="CBR Protection Layers" width="1500">

A secure cloud architecture uses the "Defense in Depth" principle and combines two fundamental protection layers:

### 1. Network-Based Protection (The Infrastructure Layer)

Here, data traffic is controlled based on **IP addresses, ports, and protocols**. It's about whether a data packet may physically arrive.

- `Security Groups`: A **stateful firewall** that sits directly at the virtual server instance (VSI). It precisely controls which traffic may reach or leave the server.
- `Access Control Lists (ACLs)`: A **stateless filter** at the subnet level. They act as the first barrier and control what may flow into or out of the subnet at all.

### 2. Identity-Based Protection (The Logic Layer)

Here, access is controlled based on **identities and context**. It's about whether a user or service may perform an action (API call), even if they have network access.

- `IAM`: Controls the **"Who" and "What"**. It authenticates the user and checks if they have the necessary rights (roles).
- `Context-Based Restrictions (CBR)`: Links identity with the network. It checks whether the authenticated user is also coming from an allowed network.

**Summary:**

- **Network Protection** prevents unwanted data packets from reaching your servers (e.g., hacker port scans)
- **Identity Protection** prevents authenticated users from performing unauthorized actions or stolen credentials from being used from insecure locations

---

# 4. Working with Resources

## 4.1 Navigating the Catalog

The catalog is the central marketplace and entry point for all services and software solutions in IBM Cloud. It serves to discover, select, and provision resources.

**The content is divided into four main areas:**

- **Services:** IBM-managed services (Managed Services) such as databases, storage, or compute resources
- **Software:** Installable components such as container images, Helm charts, or operators (e.g., for OpenShift), from both IBM and certified third-party providers
- **Deployable Architectures:** Pre-built infrastructure templates (IaC) to set up complex environments securely and compliantly
- **Professional Services:** Consulting and implementation services. Here you find expert support from IBM or partners for specific projects such as migrations, architecture design, or modernization projects

**Additionally:**

**Private Catalog:** Companies can create private catalogs. These serve to provide their own software solutions or approved versions of public services internally for teams and centrally control their access.

**To access the catalog, proceed as follows:**

1. Click on `Catalog` in the top bar
2. Browse through the offering of over 300 products via the search bar or use the various filter options

<img src="{{ site.baseurl }}/screenshots/catalog1.png" alt="Catalog Overview" width="1500">

---

## 4.2 Provisioning Resources from the Catalog

Once you have found the desired service in the catalog, perform the following steps for provisioning:

**Select Service:** Search for the resource name and click on the corresponding tile. You will now reach the service configuration page.

**Obtain Information:** Before creating the resource, you can inform yourself via the tabs in the upper area:

- **About:** Here you will find an overview of features, available plans, and pricing models
- **Docs:** This link takes you directly to the official technical documentation to learn details about setup and usage

**Check Configuration & Price:** Select your desired region and pricing plan. Pay attention to the right sidebar. There you will see a dynamic cost estimate (Cost Summary). Depending on the service and plan, the price can be shown in different intervals (e.g., Hourly for short-term use or Monthly for long-term calculations).

**Create:** Once you have made all settings and agree with the displayed price, complete the process with a click on the `Create` button. The resource will now be provisioned.

<img src="{{ site.baseurl }}/screenshots/catalog2.png" alt="Catalog Service Configuration" width="1500">

---

## 4.3 Managing / Deleting Resources

To get an overview of provisioned resources/services, navigate as follows:

1. Click on the `Hamburger Menu (Navigation Menu)` in the top left
2. Select the `Resource list` option

In the now displayed overview, you have various options to efficiently organize your resources:

- You can **filter the list specifically by name or resource groups** to find specific services faster
- Additionally, you have the **option to edit tags or delete resources directly from the list**
- Clicking on a resource name opens its individual dashboard. There you access the detailed menu to further **configure, edit, or permanently remove the instance**

<img src="{{ site.baseurl }}/screenshots/catalog4_.png" alt="Resource List" width="1500">

<img src="{{ site.baseurl }}/screenshots/catalog3.png" alt="Resource Management" width="1500">

---

# 5. Billing and Usage

## 5.1 Billing and Usage Overview

The central entry point for cost management is the Overview page. It provides a projected summary of your account's current financial status without immediately diving into complex data tables.

**Key metrics at a glance:**

- **Usage summary:** Shows the costs of past months, the estimated total costs for the current month to date, and a cost forecast for the coming month
- **Recent Invoices:** A list of invoices from recent months including amount and payment status
- **Billing Period:** Indicates the start and end date of the current billing cycle
- **Commitments & Subscriptions:** An overview of contractual minimum commitments, subscriptions, or available credit
- **Spending notifications:** Shows the status of your configured alerts (e.g., whether budget limits are almost reached)

**Navigation to Billing and Usage:**

1. Click on `Manage` in the top bar
2. Select `Billing and usage`
3. You land by default directly on the `Overview` tab

<img src="{{ site.baseurl }}/screenshots/billingandusage1.png" alt="Billing Overview" width="1500">

---

## 5.2 Usage

The Usage area is your primary tool for validating the monthly invoice. It allows you to precisely break down costs to resource groups and trace them down to individual technical metrics.

**Navigation:** Select the `Usage` option in the left menu under `Billing and usage`

<img src="{{ site.baseurl }}/screenshots/billingandusage2.png" alt="Usage Overview" width="1500">

### The Analysis Workflow (Drill-down)

Proceed as follows to check cost generation in detail:

**Select Time Period and Grouping:**

Select the desired month in the top right. Then change the view at "Group by" to the desired Resource Group.

**Result:** You immediately see what costs the selected resource group incurred in this month.

<img src="{{ site.baseurl }}/screenshots/billingandusage3.png" alt="Usage by Resource Group" width="1500">

**Check Usage by Service, Plan, and Region:**

Click on `View plans` to view the usage of a service (You can also directly select a service in the `Usage` start view and go to `View plans`).

**Result:** You see at a glance the used plan (e.g., Standard or Enterprise) and the region (e.g., Frankfurt) where the costs were incurred. You can also apply the filter here to a specific month and resource group.

<img src="{{ site.baseurl }}/screenshots/billingandusage4.png" alt="Usage by Service" width="1500">

<img src="{{ site.baseurl }}/screenshots/billingandusage5.png" alt="Usage by Plan" width="1500">

**Analyze Consumption Units:**

Click on `View details` for a service.

**Result:** Here you see the complete breakdown of billing metrics for this service. You can see exactly what was charged, e.g.:

- GIGABYTE_HOURS (How much storage was occupied for how long?)
- MILLION_API_CALLS (How often was the service accessed?)
- IP_HOURS (Costs for reserved IPs)

<img src="{{ site.baseurl }}/screenshots/billingandusage6_.png" alt="Consumption Units" width="1500">

<img src="{{ site.baseurl }}/screenshots/billingandusage7.png" alt="Billing Metrics" width="1500">

**Deep Analysis at Instance Level:**

To know exactly which specific instance (resource group) is responsible for which costs and how exactly the costs are broken down, click on `View instance details`.

**Result:** You drill down one more level. Now you see each individual instance (resource group) and its individual contribution to the total costs.

**Summary:** In the Usage area, you move from "big to small": From the resource group via the service plan to the technical metrics and finally to the individual instance.

<img src="{{ site.baseurl }}/screenshots/billingandusage8.png" alt="Instance Details" width="1500">

<img src="{{ site.baseurl }}/screenshots/billingandusage9.png" alt="Cost Breakdown" width="1500">

**Tip:** You can export the expenses of all levels as CSV by clicking on `Export CSV` in the upper right field.

---

## 5.3 Cost Analysis

Cost Analysis serves to strategically examine your expenses. It provides you with powerful tools to not only see totals, but to isolate cost drivers through precise filtering and visualize them.

**Navigation:** Select the `Cost analysis` option in the left menu under Billing and usage

### Functions and Filters

To tailor the cost analysis precisely to your question, the sidebar offers a variety of filters. You can restrict the display by the following categories, among others:

- `Region`
- `Service`
- `Plan`
- `Instance & Instance ID`
- `Resource group`
- `Category`
- `Tags`
- ...and other specific criteria

**Time frame:** Via the Time frame dropdown menu, you determine the observation period (e.g., 3 months, 6 months) to compare developments over a longer period.

**Group by:** At the top, you can specify via Group by how the data should be summarized in the chart (e.g., costs grouped by resource group or service) to immediately capture trends visually.

<img src="{{ site.baseurl }}/screenshots/costanalysis.png" alt="Cost Analysis" width="1500">

**Difference from Usage:**

The crucial difference lies in the time reference and visualization.

While the Usage area provides you with a static, tabular billing for a single month (focus: invoice verification), Cost Analysis visualizes the development over several months (focus: trend detection). You use **Usage** to see exactly **"what" was charged**, and **Cost Analysis** to understand **"how" costs are developing**.

---

## 5.4 Spending Notifications

So you don't have to actively check the dashboard daily, IBM Cloud offers Spending Notifications. These are automatic alerts that inform you via email as soon as your expenses reach a defined threshold.

**How to create a notification:**

1. Navigate to `Manage` > `Billing and usage`
2. Select the `Spending notifications` option in the left menu
3. Click on the `Create` button

<img src="{{ site.baseurl }}/screenshots/spending_notifications1.png" alt="Spending Notifications" width="1500">

### Configuring the Alert

- **Service:** Decide for which service the notification should apply
- **Recipients:** Enter the email addresses of the people who should be notified (e.g., the Account Owner or project manager)
- **Threshold:** Set a monetary amount (e.g., 500 USD). You can then set at what percentage of this amount to be warned (e.g., notification at 80%, 90%, and 100% of the budget)

Finally confirm the setup with a click on `Create`.

<img src="{{ site.baseurl }}/screenshots/spending_notifications2.png" alt="Configure Spending Notifications" width="1500">

---

# 6. Enterprise Accounts

## 6.1 Enterprise Account Basics

An Enterprise Account is an **administrative hierarchy** that enables large organizations to consolidate multiple IBM Cloud Accounts under one central umbrella. This significantly simplifies management, billing, and governance.

<img src="{{ site.baseurl }}/screenshots/EnterpriseAccountArch.png" alt="Enterprise Account Architecture" width="1200">

### The advantages and functions are divided into three main areas:

### Centralized Billing & Cost Management

The Enterprise Account acts as the central payment point for all subordinate accounts.

**Consolidated Invoice:** Instead of many individual invoices, you receive a single, consolidated invoice for the entire company.

**Credit Pooling:** Subscription Credits (credit) are collected at the Enterprise level in a common pool. All accounts in the hierarchy draw from this pool to cover their "Entitlements". This prevents credit from expiring in one account while another account has to pay extra.

**Downstream visibility:** Although the invoice is paid centrally, the system offers full transparency about the consumption of individual accounts. The company can thus precisely determine which department or project caused which costs and charge them internally.

<img src="{{ site.baseurl }}/screenshots/EnterpriseAccountCreditPool.png" alt="Credit Pooling" width="1200">

### Flexible Account Hierarchy

You can map your company's structure exactly in the cloud.

**Account Integration:** You have the flexibility to create completely new accounts at any time or subsequently import existing accounts into the Enterprise hierarchy.

**Resource Usage:** It's important to understand that the actual resources (servers, databases) continue to be consumed and operated at the account level. ***The Enterprise Account only serves management purposes.***

**Unified Support:** The support level (e.g., Premium or Advanced) is set centrally and automatically applies to every account within the hierarchy.

<img src="{{ site.baseurl }}/screenshots/EnterpriseAccountRessources2.png" alt="Account Hierarchy" width="1200">

<img src="{{ site.baseurl }}/screenshots/EnterpriseAccountRessources.png" alt="Resource Management" width="1200">

### Governance and Security

The Enterprise Account provides a central control level for policies.

**Central Policies:** You can define governance rules and access policies (IAM) centrally and inherit them downward. This ensures that security standards are maintained company-wide without having to configure each account individually.

<img src="{{ site.baseurl }}/screenshots/EnterpriseAccountGovernance.png" alt="Governance" width="1200">

---

## 6.2 Enterprise Account Example Architectures

### Automotive Manufacturer

<img src="{{ site.baseurl }}/screenshots/EnterpriseAccountCarco_.png" alt="Automotive Example" width="1200">

### Business Partner with End Customers

<img src="{{ site.baseurl }}/screenshots/EnterpriseAccountBP_.png" alt="Business Partner Example" width="1000">

---

# 7. Additional Information

## 7.1 Support Center

The Support Center is your central point of contact for all technical inquiries, problem reports, and assistance regarding the IBM Cloud Platform and its services.

**Navigation:** Click on `Help` in the top navigation bar and then the `Support center` menu item

### The most important functions:

- **Case Management (Tickets):** Here you can create new support cases ("Cases") when you encounter technical problems. The processing time depends on the severity and your support plan

- **FAQs & Documentation:** Before opening a ticket, you can use the integrated search to research known solutions and best practices in the knowledge base

<img src="{{ site.baseurl }}/screenshots/SupportCenter.png" alt="Support Center" width="1250">

---

## 7.2 Importance of Notifications

In a dynamic cloud environment, regularly checking notifications ***(bell icon in the top right)*** is not an optional task, but an operational necessity.

Ignoring these messages can have serious consequences for the stability of your applications.

**IBM Cloud uses this channel for critical information:**

### Deprecations

Cloud services and runtimes are constantly evolving. When a specific database version or software component reaches its "End of Life", you are warned here in advance. If you overlook this warning, your application may stop working or can no longer be deployed from one day to the next.

### Planned Maintenance

You receive information about upcoming updates to the physical infrastructure or services. This gives you time to check high-availability mechanisms or schedule maintenance windows.

### Required Actions

Often security updates require an active action on your part (e.g., "Restart the cluster to apply the security patch").

**Recommendation:** Regularly check the Notification Center for messages in the High or Critical categories to avoid unplanned outages ("Silent Failures").

**Additionally:**

**Cloud Status:** Via the Support Center > `View cloud status` you reach the central dashboard for monitoring the entire IBM Cloud Platform. Here you not only check the current availability of all services (Overview), but also gain insight into **planned maintenance** (Planned maintenance), **critical security warnings** (Security bulletins), **root cause reports on past incidents** (Incident reports), as well as **Release Notes** and **Announcements**.

<img src="{{ site.baseurl }}/screenshots/Notifications.png" alt="Notifications" width="1500">

---

## 7.3 Cost Estimations

The Cost Estimator is an integrated planning tool that allows you to forecast monthly costs for your planned infrastructure before provisioning resources. It's ideal for budget planning or obtaining approvals.

**How to use the tool:**

### In the Catalog

When you configure a service, you see the current price estimate in the right sidebar. Instead of clicking directly on Create, select the `Add to estimate` button. This adds the configuration to your preliminary shopping cart.

### Review Estimate

Click on the calculator icon (Cost estimator) in the top header of the console. Here you see the collected list of all added services.

### Functions in the Overview

- **Adjustment:** You can subsequently change quantities (e.g., number of servers or GB storage) to simulate different scenarios
- **Currency:** Set the display to your local currency
- **Export:** Via the Download CSV/XLSX or Print/PDF button, you can generate an official cost estimate to forward it, for example, to the finance department for approval

<img src="{{ site.baseurl }}/screenshots/CostEstimator.png" alt="Cost Estimator" width="1500">

---

## 7.4 Documentation

The [official documentation](https://cloud.ibm.com/docs) is your most important knowledge source. It provides technical references that are essential for secure operation.

**How to access the documentation:**

You have two ways to access the content:

### Global

Click on the `Docs` entry under the `? Symbol` in the top header of the console. This leads you to the central start page with a search across all services.

### Context-specific

If you are currently in th