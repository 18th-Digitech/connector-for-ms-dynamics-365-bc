# Installation Guide
Connector for MS Dynamics 365 BC

This document provides step-by-step instructions to install, configure, and deploy the Connector for MS Dynamics 365 BC App using Adobe App Builder.

---

## 1. Prerequisites

### System Requirements
- Node.js v18+
- Adobe I/O CLI v10+ (installed and authenticated)

### Access Requirements
- Adobe App Builder
- Adobe Developer Console
- Adobe Commerce Admin

### Credentials Required
- Business Central Environment 
- Business Central Host
- Business Central Tenant
- Business Central Company
- Business Central Oauth Client
- Business Central Oauth Secret
- Business Central Oauth Grant Type


## 2.Quick Start Installation
1. Download the Connector for MS Dynamics 365 BC App code from Adobe Exchange
2. Create an App Builder Project in Developer Console
3. Update your Environment Variables
4. Initialize and Deploy App Builder Actions to the workspace and subscribe to Commerce events

---

## 3. Install the App from Adobe Exchange

1. Acquire the Microsoft Dynamics 365 Business Central  App from Adobe Exchange
2. Obtain organization admin approval
3. Select environment (Development / Staging / Production)
4. Create workspace using the guide:
   https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/

---

## 4. Configure Required Services

Create an App Builder Project in Developer Console along with required services.


1. Log in to the and select the desired organization from the dropdown menu in the top-right cornerAdobe Developer Console
2. Click Create new project from template
3. Select App Builder . The Set up templated project pages displays
4. Specify a project title and app name. Mark the Include Runtime with each workspace checkbox.
5. Create workspaces (Stage/Production)
6. Add following APIs to the workspace:
   a. I/O Events
   b. I/O Management API
   c. Adobe I/O Events for Adobe Commerce
   d. Adobe Commerce as a Cloud Service (For SaaS installatio)

## 5. Environment Configuration

### 5.1 Create .env File

```bash
cp .env.dist .env
```

Run this command in the project root directory.

---

### 5.2 Adobe Commerce Configuration

```env
COMMERCE_BASE_URL=https://<your-commerce-url>/rest/
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=
```

---

### 5.3 Business Central Configuration

```env
BC_ENVIRONMENT=
BC_HOST=
BC_TENANT=
BC_COMPANY=
BC_OAUTH_CLIENT=
BC_OAUTH_SECRET=
BC_OAUTH_SCOPES=
BC_OAUTH_GRANT_TYPE
```

---

### 5.4 Custom Environment Variable 

# Inventory sources
AVAILABLE_SOURCES_DIR=sources_data/

# All SKUs
AVAILABLE_SKU_DIR=catalog_data/

# Attribute Options
AVAILABLE_ATTRIBUTE_OPTIONS=attributeOptions/

# AttributeCode
PRODUCT_ATTRIBUTE_CODE=uom$UOM$option

# Product Constant Values
TAX_CLASS_ID=2
WEBSITE_IDS=1

### 5.5 Adobe App Builder (IMS OAuth – SaaS)

```env
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
OAUTH_SCOPES=['…']
OAUTH_HOST=https://ims-na1.adobelogin.com
```

---

### 5.6 Workspace Identifiers

Copy from Developer Console → Project → Workspace:

```env
IO_CONSUMER_ID=
IO_PROJECT_ID=
IO_WORKSPACE_ID=
```

---

### 5.7 Add workspace.Json file

The workspace.json file must be placed in  scripts/onboarding/config/
https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/#download-the-workspace-configuration-file


## 6. Authentication: PaaS vs SaaS

### Base URL Differences

- PaaS: https://<env>.magentosite.cloud/rest/
- SaaS: https://na1-sandbox.api.commerce.adobe.com/<tenant-id>/

### Authentication Precedence

- OAuth1 (PaaS) is used if COMMERCE_* variables are set
- IMS OAuth (SaaS) is used if COMMERCE_* variables are empty

---

## 7. Obtain Credentials

### Adobe Commerce (PaaS)
- System → Extensions → Integrations → Add New Integration
- Grant API access and activate integration

### Shipsy
- Log in to Microsoft Dynamics 365 Business Central
- Request API credentials from Business Central support if required

### Adobe App Builder
- Developer Console → Project → Workspace → OAuth Server-to-Server

---

## 8. Initialize 

```bash
npm install
aio login
aio console org select
aio console project select
aio console workspace select
aio app use --merge
```

## 9 Onboarding & Deploy

The onboarding script must be executed manually before running aio app deploy. If this step is skipped, the post-deploy script may fail.

```bash
npm run onboard

```
### 9.1 Deploy

```bash
aio app deploy

```


## 10. Event Subscription

### Event Used
- observer.customer_save_commit_after

### Subscribe Manually (if needed)

```bash
npm run commerce-event-subscribe
```

Event subscriptions are automatically created during deployment.

---

## 11. Testing

-Run Full Product Sync → Entire catalog updates in Adobe Commerce
-Execute Delta Sync → Recently modified products are updated
-Perform Specific Sync → Selected products sync successfully
-Run Source Sync → Inventory sources update correctly
-Update customer in My Account → Customer data syncs to Business Central (if exists)

---

## 12. Debugging & Monitoring

Developer Console → Events → Commerce Customer Sync → Debug Tracing

More details:
https://developer.adobe.com/commerce/extensibility/app-development/best-practices/logging-troubleshooting/#event-logs

---

## 13. Troubleshooting

-Customer sync issues: If customer data is not syncing, go to Developer Console → Events → Commerce Customer Sync → Debug Tracing to review event
 logs and identify errors.
-Product or Inventory Source sync errors: Navigate to your project directory and run aio rt:activation:list to view recent activations. Identify
 the relevant activation ID for the failed sync, then run aio rt:activation:log <activationId> to retrieve detailed error logs.
-General sync failures: Verify API credentials, environment configurations, and ensure scheduled cron jobs are running correctly.

---

## 14. References

- https://developer.adobe.com/app-builder/docs/
- https://developer.adobe.com/commerce/extensibility/starter-kit/integration/
- https://developer.adobe.com/events/docs/support/tracing
- https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-config#

